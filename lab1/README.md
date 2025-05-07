## 1- Install k8s cluster (minikube)
![image](https://github.com/user-attachments/assets/2ece9d66-b4b0-466b-b757-75e3bc30bfc4)
<br>

## 2- Create a pod with the name redis and with the image redis.
![image](https://github.com/user-attachments/assets/85e31dc4-db5a-4827-8939-2dbfa26c7960)
<br>
<img width="163" alt="image" src="https://github.com/user-attachments/assets/0e9a3614-ff69-4ec1-b1f8-c20bd9f0d421" />
<br>

## 3- Create a pod with the name nginx and with the image “nginx123” , Use a pod-definition file.
<img width="268" alt="image" src="https://github.com/user-attachments/assets/69fc4f72-f2fb-4e07-b20e-46e1ecdf369f" />
<br>
<img width="124" alt="image" src="https://github.com/user-attachments/assets/bbfec9f9-ac32-43ec-9d76-f2b111216641" />
<br>
<img width="333" alt="image" src="https://github.com/user-attachments/assets/f8367731-2a0d-48c7-a512-085faab40df7" />
<br>

## 4- What is the nginx pod status?
<img width="275" alt="image" src="https://github.com/user-attachments/assets/c66ca0c5-7849-4651-bf7f-2e27f7b49a4b" />
<br>

## 5- Change the nginx pod image to “nginx” check the status again
<img width="153" alt="image" src="https://github.com/user-attachments/assets/98c285fd-aa48-4eec-b393-a1be6c83613c" />
<br>
<img width="283" alt="image" src="https://github.com/user-attachments/assets/a968fed5-defc-4f30-8cb8-68da5428af11" />
<br>

## 6- How many ReplicaSets exist on the system?
<img width="273" alt="image" src="https://github.com/user-attachments/assets/a8fa496b-3a3e-41a1-a988-7e8979794a63" />
<br>

## 7- Create a ReplicaSet with name= replica-set-1 , image= busybox , replicas= 3
<img width="307" alt="image" src="https://github.com/user-attachments/assets/9104c314-1731-469c-abad-7d40fd5a02a7" />
<br>
<img width="327" alt="image" src="https://github.com/user-attachments/assets/b7c0e2e8-3c3d-4b76-9f73-928bfc1f076a" />
<br>
<img width="357" alt="image" src="https://github.com/user-attachments/assets/adfc0b85-1036-4dca-8270-234301e2e959" />
<br>
<img width="267" alt="image" src="https://github.com/user-attachments/assets/d807e458-cba9-49de-8b54-68245565e64d" />
<br>

## 8- Scale the ReplicaSet replica-set-1 to 5 PODs.
<img width="395" alt="image" src="https://github.com/user-attachments/assets/98bd96f0-d9cc-49f9-8e4a-fa19586d19ac" />
<br>
<img width="270" alt="image" src="https://github.com/user-attachments/assets/a08e4615-32ac-442e-a840-2175ecc62f1f" />
<br>

## 9- How many PODs are READY in the replica-set-1?
<img width="294" alt="image" src="https://github.com/user-attachments/assets/90f31c49-8b7b-4ecf-93d9-fe690db1a078" />
<br>

## 10- Delete any one of the 5 PODs then check How many PODs exist now? & Why are there still 5 PODs, even after you deleted one?
Still the same because ReplicaSet checks on them all the time to ensure there are five, and if one is deleted, it will create a new one.
<img width="376" alt="image" src="https://github.com/user-attachments/assets/5a89b985-40d0-4829-b294-d33527c020d2" />
<br>
<img width="307" alt="image" src="https://github.com/user-attachments/assets/115bc1a1-71a8-415d-8751-7f1b1079533a" />
<br>

 ## 11- How many Deployments and ReplicaSets exist on the system?
 <img width="406" alt="image" src="https://github.com/user-attachments/assets/a51206b7-686e-4f35-8d46-7ce876cedd0d" />

 ## 12- create a Deployment with
 name= deployment-1
 image= busybox
 replicas= 3
 <br>
 <img width="200" alt="image" src="https://github.com/user-attachments/assets/8652c791-6ded-448a-88b1-323095ec82e4" />
 <br>
 <img width="381" alt="image" src="https://github.com/user-attachments/assets/720d09ff-48d3-4249-beac-06a28998cc51" />
 <br>
 ## 13- How many Deployments and ReplicaSets exist on the system now?
 <img width="312" alt="image" src="https://github.com/user-attachments/assets/8b983422-bef9-44c8-ae5f-162ce63e6488" />

 ## 14- How many pods are ready with the deployment-1?
 <img width="331" alt="image" src="https://github.com/user-attachments/assets/eea5721c-ff20-4dee-999f-c20e94cc47e3" />

 ## 15- Update deployment-1 image to nginx then check the ready pods again
 <br>
 <img width="411" alt="image" src="https://github.com/user-attachments/assets/99c1a31f-de73-4a98-9d79-fb5ede9c6b89" />
 <br>
 <img width="352" alt="image" src="https://github.com/user-attachments/assets/5329941a-d9aa-4855-bdf0-2ab4f9cd347b" />

 ## 16- Run kubectl describe deployment deployment-1 and check events
 What is the deployment strategy used to upgrade the deployment-1?
 <br>
 <img width="388" alt="image" src="https://github.com/user-attachments/assets/9de26baf-7a52-4144-81c9-f08c8dcefb57" />
 <br>
 <img width="191" alt="image" src="https://github.com/user-attachments/assets/f1da2a21-2252-4107-a743-d0bcbb580828" />
 <br>
 
 ## 17- Rollback the deployment-1
 What is  the used image with the deployment-1?
 <br>
 <img width="442" alt="image" src="https://github.com/user-attachments/assets/f82f72b3-bfe0-4425-9647-5da812f82057" />
 <br>
 ## 18- Create a deployment using nginx image with latest tag only and remember to
 mention tag i.e nginx:latest and name it as nginx-deployment. App labels should be
 app: nginx-app and type: front-end. The container should be named as
 nginx-container; also make sure replica counts are 3.
 <br>
 <img width="399" alt="image" src="https://github.com/user-attachments/assets/3348e193-35d2-49ee-b6b0-b4275c1b8a42" />
 <br>
 <img width="414" alt="image" src="https://github.com/user-attachments/assets/8fc58c92-84d7-4989-be17-9f5bb999d0cd" />
