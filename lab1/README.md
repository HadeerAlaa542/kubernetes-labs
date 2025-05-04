 ## 1- Install k8s cluster (minikube)
 ![image](https://github.com/user-attachments/assets/2ece9d66-b4b0-466b-b757-75e3bc30bfc4)

 ## 2- Create a  pod with the name redis and with the image redis.
 ![image](https://github.com/user-attachments/assets/85e31dc4-db5a-4827-8939-2dbfa26c7960)
 
 <img width="163" alt="image" src="https://github.com/user-attachments/assets/0e9a3614-ff69-4ec1-b1f8-c20bd9f0d421" />

 ## 3-  Create a  pod with the name nginx and with the image “nginx123”
 Use a pod-definition file.
 <img width="268" alt="image" src="https://github.com/user-attachments/assets/69fc4f72-f2fb-4e07-b20e-46e1ecdf369f" />
 
 <img width="124" alt="image" src="https://github.com/user-attachments/assets/bbfec9f9-ac32-43ec-9d76-f2b111216641" />
 
 <img width="333" alt="image" src="https://github.com/user-attachments/assets/f8367731-2a0d-48c7-a512-085faab40df7" />

 ## 4- What is the nginx pod status?
 <img width="275" alt="image" src="https://github.com/user-attachments/assets/c66ca0c5-7849-4651-bf7f-2e27f7b49a4b" />

 ## 5- Change the nginx pod image to “nginx” check the status again
 <img width="153" alt="image" src="https://github.com/user-attachments/assets/98c285fd-aa48-4eec-b393-a1be6c83613c" />
 
 <img width="283" alt="image" src="https://github.com/user-attachments/assets/a968fed5-defc-4f30-8cb8-68da5428af11" />

 ## 6- How many ReplicaSets exist on the system?
 <img width="273" alt="image" src="https://github.com/user-attachments/assets/a8fa496b-3a3e-41a1-a988-7e8979794a63" />

 ## 7- create a ReplicaSet with
 name= replica-set-1
 image= busybox
 replicas= 3
 <img width="307" alt="image" src="https://github.com/user-attachments/assets/9104c314-1731-469c-abad-7d40fd5a02a7" />
 
 <img width="327" alt="image" src="https://github.com/user-attachments/assets/b7c0e2e8-3c3d-4b76-9f73-928bfc1f076a" />
 
 <img width="357" alt="image" src="https://github.com/user-attachments/assets/adfc0b85-1036-4dca-8270-234301e2e959" />
 
 <img width="267" alt="image" src="https://github.com/user-attachments/assets/d807e458-cba9-49de-8b54-68245565e64d" />

 ## 8- Scale the ReplicaSet replica-set-1 to 5 PODs.
 <img width="395" alt="image" src="https://github.com/user-attachments/assets/98bd96f0-d9cc-49f9-8e4a-fa19586d19ac" />
 
 <img width="270" alt="image" src="https://github.com/user-attachments/assets/a08e4615-32ac-442e-a840-2175ecc62f1f" />

 ## 9- How many PODs are READY in the replica-set-1?
 <img width="294" alt="image" src="https://github.com/user-attachments/assets/90f31c49-8b7b-4ecf-93d9-fe690db1a078" />

 ## 10- Delete any one of the 5 PODs then check How many PODs exist now?
 Why are there still 5 PODs, even after you deleted one?
 <img width="376" alt="image" src="https://github.com/user-attachments/assets/5a89b985-40d0-4829-b294-d33527c020d2" />
 
 <img width="307" alt="image" src="https://github.com/user-attachments/assets/115bc1a1-71a8-415d-8751-7f1b1079533a" />

# still the same because replicset check on them all the time that they five and if not it will create the deleted
