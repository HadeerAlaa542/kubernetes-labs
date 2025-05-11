# Lab 26: Updating Applications and Rolling Back Changes

## 🧪 Objective

Learn how to:
- Deploy an application in Kubernetes
- Expose it using a service
- Access it locally via port forwarding
- Update the application
- View rollout history
- Roll back to a previous version
- Monitor pod status

---

## 📁 Files

- `nginx-deployment.yaml` — Initial deployment of NGINX with 3 replicas.
- `nginx-service.yaml` — ClusterIP or NodePort service to expose NGINX.  
---

## 🔧 Steps

### 1. Deploy NGINX with 3 Replicas

```bash
kubectl apply -f nginx-deployment.yaml
````
![image](https://github.com/user-attachments/assets/1cc2279e-e267-490a-b4e8-382299d1a28c)

Verify deployment:

```bash
kubectl get deploy
```
![image](https://github.com/user-attachments/assets/a9efa1c7-f771-49e3-ab80-9ef6707a3a77)

---

### 2. Create a Service to Expose the Deployment

```bash
kubectl apply -f my-service.yaml
```
![image](https://github.com/user-attachments/assets/ff2f9222-7dd2-469b-818e-901a960982e7)

Check the service:

```bash
kubectl get svc
```
![image](https://github.com/user-attachments/assets/1f6bf45d-4d6c-4f7b-8616-a5cae1660228)

---

### 3. Access the Service

* If using **ClusterIP**:

```bash
kubectl port-forward svc/my-service 7070:80
```
![image](https://github.com/user-attachments/assets/6dbcc011-510c-44c7-b38e-79fee3a14078)

Visit: [http://localhost:8080](http://localhost:8080)

![image](https://github.com/user-attachments/assets/e63c87a8-c246-4647-b6a0-5d155fb33f41)

---

### 4. Update the Deployment (e.g., change image to Apache)

```bash
kubectl edit deploy nginx-deployment 
```
![image](https://github.com/user-attachments/assets/78ce87ca-5b30-4593-9334-55a7190e5b53)

![image](https://github.com/user-attachments/assets/b53cbcc7-d3e2-4495-9587-584170228efa)

![image](https://github.com/user-attachments/assets/638c14b3-21cc-4cb0-bfec-a902ee01b5ea)

### 5. View Rollout History

```bash
kubectl rollout history deployment/nginx-deployment
```
![image](https://github.com/user-attachments/assets/b0d338c1-ea71-4052-9845-3e090dac1e0a)

---

### 6. Roll Back to Previous Version

```bash
kubectl rollout undo deployment/nginx-deployment
```
(Optional: Roll back to a specific revision)

```bash
kubectl rollout undo deployment/web-server --to-revision=1
```
![image](https://github.com/user-attachments/assets/5aade672-8128-445b-82c5-76e45aa47f6e)

---

### 7. Monitor Pod Status

```bash
kubectl rollout status deployment/web-server
```
![image](https://github.com/user-attachments/assets/812188ec-6d2e-412b-9540-5833b7b2da0e)

![image](https://github.com/user-attachments/assets/a5f6f7cd-8466-4ed8-93cd-c4b2f0f39455)

![image](https://github.com/user-attachments/assets/0656270f-3180-4f23-b804-e31fa0037b5c)

---

## ✅ Outcome

By the end of this lab, you should be comfortable with:

* Managing updates in a Kubernetes deployment
* Tracking changes through rollout history
* Using rollback to restore stable versions

```
