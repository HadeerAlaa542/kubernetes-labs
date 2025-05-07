# Lab 2: Kubernetes Namespace, Nodes, and Affinity

This lab covers namespace and pod inspection, deployment creation with resource limits, node inspection, labeling, taints, and node affinity for scheduling.

---

## 🧪 1. How many Namespaces exist on the system?

```bash
kubectl get namespaces
````

**Result:**

<img width="305" alt="image" src="https://github.com/user-attachments/assets/e55ebc05-757d-4171-8675-e579803a317b" />

---

## 🧪 2. How many pods exist in the `kube-system` namespace?

```bash
kubectl get pods -n kube-system
```

**Result:** 

<img width="440" alt="image" src="https://github.com/user-attachments/assets/7b6ab5cb-c8de-4706-8f8f-6a3f640dab21" />

---

## 🏗️ 3. Create a Deployment in the `finance` Namespace

**Namespace creation:**

```bash
kubectl create namespace finance
```
<img width="436" alt="image" src="https://github.com/user-attachments/assets/be0f7352-a7e5-4677-9094-8520b6b5aecd" />

**Deployment YAML:**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: beta
  namespace: finance
spec:
  replicas: 2
  selector:
    matchLabels:
      app: beta
  template:
    metadata:
      labels:
        app: beta
    spec:
      containers:
      - name: redis
        image: redis
        resources:
          requests:
            memory: "1Gi"
            cpu: "500m"
          limits:
            memory: "2Gi"
            cpu: "1"
```

✅ Created successfully using:

```bash
kubectl apply -f finance-deployment.yaml
```
<img width="435" alt="image" src="https://github.com/user-attachments/assets/a5ec91b0-97ca-45a2-831e-852fbca72bc6" />
<img width="442" alt="image" src="https://github.com/user-attachments/assets/80341c92-7cdd-4728-aa28-719a4e0f7719" />

---

## 🧮 4. How many Nodes exist on the system?

```bash
kubectl get nodes
```

**Result:**

<img width="443" alt="image" src="https://github.com/user-attachments/assets/a9146332-ba9d-44de-8543-6af70c5e0ad6" />

---

## 🔍 5. Do you see any taints on master?

```bash
kubectl describe node minikube | grep -i taint
```

**Result:**

```
Taints: node-role.kubernetes.io/control-plane:NoSchedule
```

✅ Master has a taint.

---

## 🏷️ 6. Apply a label `color=blue` to the master node

```bash
kubectl label node minikube color=blue
```

✅ Verified with:

```bash
kubectl get nodes --show-labels
```

---

## 🚀 7. Create a deployment named `blue` with nginx and node affinity

**Deployment YAML:**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: blue
  template:
    metadata:
      labels:
        app: blue
    spec:
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: color
                operator: In
                values:
                - blue
      containers:
      - name: nginx
        image: nginx
```

✅ Applied using:

```bash
kubectl apply -f blue-deployment.yaml
```

---

