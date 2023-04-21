# proj3

Docker command: 
Minibube command: 

minikube start 
kubectl apply -f flask-app-pod.yaml
kubectl apply -f mongodb-pod.yaml


kubectl apply -f mongo-deployment.yaml  
kubectl apply -f flask-deployment.yaml

kubectl apply -f mongodb-service.yaml
kubectl apply -f flask-app-service.yaml      
minikube service flask-app-service --url          

