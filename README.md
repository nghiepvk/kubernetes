# Kubernetes  

## Launch Single Node Kubernetes Cluster  

1. Checking version of Minikube.  

    > minikube version  
    > minikube start --wait=false  
    > kubectl cluster-info  
    > kubectl get nodes  

2. Create a first deployment.  

    > kubectl create deployment first-deployment --image=katacoda/docker-http-server  
    > kubectl get pods  
    > kubectl expose deployment first-deployment --port=80 --type=NodePort  

3. Verify first deployment.

    > export PORT=$(kubectl get svc first-deployment -o go-template='{{range.spec.ports}}{{if .nodePort}}{{.nodePort}}{{"\n"}}{{end}}{{end}}')  
    >> echo "Accessing host01:\$PORT"  
    >> curl host01:\$PORT
4. Enable Dashboard.

    > minikube addons enable dashboard  
    > kubectl apply -f /opt/kubernetes-dashboard.yaml  
    > kubectl get pods -n kubernetes-dashboard -w  

## Start containers using Kubectl

1. Run a container.

    > kubectl run http --image=katacoda/docker-http-server:latest --replicas=1  
    > kubectl get deployments  
    > kubectl describe deployment http  

2. Expose port out.

    > kubectl expose deployment http --external-ip="172.17.0.17" --port=8000 --target-port=80  
    > curl <http://172.17.0.17:8000>  

