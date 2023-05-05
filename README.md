# proj3


part2: 
docker build -t alyssa7/proj3:latest .
docker-compose up
docker push alyssa7/proj3:latest


part3:
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


part5: 
kubectl delete pod ${podName}
# should genereate a new pod
kubectl get pods


part 8:
kubectl create namespace monitoring

kubectl apply -f clusterRole.yaml

kubectl apply -f config-map.yaml

kubectl apply -f prometheus-deployment.yaml

kubectl get deployments --namespace=monitoring

kubectl get pods --namespace=monitoring
kubectl port-forward ${podName} 8080:9090 -n monitoring
# Setup Kube state metrics on Kubernetes
# reference: https://devopscube.com/setup-kube-state-metrics/
git clone https://github.com/devopscube/kube-state-metrics-configs.git
kubectl apply -f kube-state-metrics-configs/
kubectl get deployments kube-state-metrics -n kube-system
# Setup alert manager on Kubernetes
# reference: https://devopscube.com/alert-manager-kubernetes-guide/#
git clone https://github.com/bibinwilson/kubernetes-alert-manager.git
kubectl apply -f kubernetes-alert-manager/
kubectl apply -f cpu_stress.yaml
# kubectl apply -f config-map.yaml

# test alert manager
kubectl get pods -n monitoring -l app=prometheus-server -o name | xargs kubectl delete -n monitoring
minikube service alertmanager --url -n monitoring

# go to the prometheus dashboard
kubectl -n monitoring port-forward svc/prometheus-service 1234:1234


part4:
 
 kubectl delete deployment flask-app-deployment
 kubectl delete deployment mongodb-deployment
 kubectl delete service flask-app-service
 kubectl delete service mongo


aws eks update-kubeconfig --region us-east-2 --name ${ClusterName}
kubectl get svc flask-app-service
kubectl port-forward service/flask-app-service 5000:5000


kubectl apply -f mongo-deployment.yaml  
kubectl apply -f flask-deployment.yaml

kubectl apply -f mongodb-service.yaml
kubectl apply -f flask-app-service.yaml
