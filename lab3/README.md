# Lab 3: Container Orchestration with Kubernetes

## Objectives
This lab focuses on deploying and managing applications using Kubernetes objects like DaemonSets, Pods, Services, and Deployments.

---

## Tasks and Steps

### 1. List all DaemonSets in all namespaces
```bash
kubectl get daemonsets --all-namespaces
````
![image](https://github.com/user-attachments/assets/02122e6a-aa01-43a5-951d-ae39eb794e49)

### 2. List DaemonSets in `kube-system` namespace

```bash
kubectl get daemonsets -n kube-system
```
![image](https://github.com/user-attachments/assets/4c77fb39-8880-428d-a886-8daa75586b21)

### 3. Identify the image used by the `kube-proxy` DaemonSet

```bash
kubectl describe daemonset kube-proxy -n kube-system
```
![image](https://github.com/user-attachments/assets/712e65b8-beb5-41b4-9a9c-f4c9daf8ec47)

### 4. Deploy FluentD Logging DaemonSet

**Name:** elasticsearch
**Namespace:** kube-system
**Image:** `k8s.gcr.io/fluentd-elasticsearch:1.20`

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: elasticsearch
  namespace: kube-system
spec:
  selector:
    matchLabels:
      name: fluentd
  template:
    metadata:
      labels:
        name: fluentd
    spec:
      containers:
      - name: fluentd
        image: k8s.gcr.io/fluentd-elasticsearch:1.20
```

Apply:

```bash
kubectl apply -f fluentd-daemonset.yaml
```
![image](https://github.com/user-attachments/assets/1cda2f3f-ed37-4b8b-982e-804f4532ef1e)

### 5. Deploy `nginx-pod` with label `tier=backend`

```bash
kubectl run nginx-pod --image=nginx:alpine --labels="tier=backend"
```
![image](https://github.com/user-attachments/assets/d4f2d192-512c-4d3d-9333-3d460aeaed6f)

![image](https://github.com/user-attachments/assets/375e6571-96cf-49f6-bc45-e8d47cf64fef)

### 6. Deploy `test-pod` using nginx:alpine

```bash
kubectl run test-pod --image=nginx:alpine --restart=Never --command -- sleep 3600
```
![image](https://github.com/user-attachments/assets/bf8adce5-97c8-4b8f-8853-0ceaceb34207)

 Or do that by using a `yaml file`.

### `test-pod.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pod
spec:
  containers:
  - name: nginx
    image: nginx:alpine
    command: ["sleep", "3600"]
```

### 7. Create ClusterIP service for `nginx-pod`

Create a **Service** named `backend-service` to expose the backend application **within the cluster** on **port 80**.

Assuming your **backend pod has the label**:

```yaml
labels:
  tier: backend
```
---

### `backend-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  selector:
    tier: backend
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
  type: ClusterIP
```
![image](https://github.com/user-attachments/assets/bea4d4ce-3e89-4b1a-89da-a67786a4fe87)

### 8. Test service accessibility from `test-pod`

```bash
kubectl exec -it test-pod -- sh
# Inside the pod
apk add curl
curl backend-service
```
![image](https://github.com/user-attachments/assets/785c3b20-edaf-4d3a-b74a-936bc09b971b)

### 9. Create Deployment `web-app` with 2 replicas

Create a **Deployment** named `web-app` using the `nginx` image with **2 replicas**.

### `web-app-deployment.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
```
![image](https://github.com/user-attachments/assets/71e933ac-2c2c-4938-af5a-9ea38ab1fb9f)

### 10. Expose `web-app` with NodePort service on port 30082

Expose the `web-app` deployment as a **Service** named `web-app-service`
on **port 80** and **NodePort 30082** so it’s accessible from outside the cluster.

---

### `web-app-service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-app-service
spec:
  selector:
    app: web-app
  type: NodePort
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30082
```
### Apply it:

```bash
kubectl apply -f web-app-service.yaml
```
![image](https://github.com/user-attachments/assets/a65fd69f-c370-4af2-b33b-46cbc4966fe2)

Then you can access it using:

```
http://<Node-IP>:30082
```

### 11. Access the web app from browser or curl

```bash
curl http://<NodeIP>:30082
```
![image](https://github.com/user-attachments/assets/3143512f-c44e-4546-a4ff-9af75bd3d1a6)

### 12. Count static pods in all namespaces**

You can identify static pods using their annotation `kubernetes.io/config.source=file`.

#### Command:

```bash
kubectl get pods -A -o jsonpath="{range .items[*]}{.metadata.name}{'\t'}{.metadata.annotations.kubernetes\.io/config\.source}{'\n'}{end}" | grep file | wc -l
```
![image](https://github.com/user-attachments/assets/ba568eb5-8acd-48d9-9a53-6bb87ff1e085)

#### Explanation:

* This filters all pods where the `config.source` is a file = **static pod**.
* `wc -l` counts how many.

---

### 13. Identify nodes running static pods**

To find which **nodes** are running those static pods:

#### Command:

```bash
kubectl get pods -A -o jsonpath="{range .items[*]}{.metadata.name}{'\t'}{.spec.nodeName}{'\t'}{.metadata.annotations.kubernetes\.io/config\.source}{'\n'}{end}" | grep file
```
![image](https://github.com/user-attachments/assets/436754e8-e490-4b62-abaf-ee2d7f2023c2)

#### Output Format:

```
<pod-name>    <node-name>    file
```

This tells you **which static pod** is running on **which node**.

---




## Summary

This lab demonstrated the use of core Kubernetes objects to orchestrate containerized applications. We deployed Pods, DaemonSets, Services, and Deployments, and learned how to test network communication between them.
