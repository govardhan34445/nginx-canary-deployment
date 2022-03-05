This repository to implement Canary deployment in kubernetes. 

1. Create configmaps for nginx version:1 and nginx version:2

       command:  kubectl apply -f nginx-1-configmap.yaml
     
     
       command:  kubectl apply -f nginx-2-configmap.yaml

2. Create nginx version 1 deployement named as "intial-deployment" with 3 no.of replicas

       command: kubectl apply -f intial-deployment.yaml 

3. Create nginx version 2 deployement named as "secondary-deployment" with 1 no.of replicas.

       command: kubectl apply -f secondary-deployment.yaml

4. create the service with common lable of "app: nginx"

        command: kubectl apply -f nginx-service.yaml

5. Access nginx app using your serverIP:NodePort. Refresh the url untill you get two version on webpage.

        To check node port use   command: kubectl get svc

6. Now Increaste the no.of replicas from 1 to 3 of secondary deployment.

        kubectl scale deploy secondary-deployment --replicas==3

6. As a final step delete the intial-deployment and now you will get the version 2 only.

        kubectl delete deploy intial-deployment
