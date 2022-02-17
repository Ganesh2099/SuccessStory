# SuccessStory

# Commands :

* kubectl api-resources

* kubectl create -f <file_name>.yaml
* kubectl apply -f <file_name>.yaml
* kubectl apply -f ./my1.yaml -f ./my2.yaml

## Node

* kubectl get nodes
* kubectl describe node <nodename>
* kubectl get nodes -o wide  

## Pod

* kubectl get pods
* kubectl get pods --show-labels
* kubectl get pods -o wide
* kubectl describe pod <pod_name>

## Service
  
* kubectl get svc
* kubectl describe svc <service_name>
* minikube service <service_name> --url

## Deployment

* kubectl apply -f deployment_definition.yml
* kubectl apply -f deployment_definition.yml --record=true
* kubectl get deployment
* kubectl describe deployment <deployment_name>
* kubectl edit deployment <deployment_name>
* kubectl delete deployment <deployment_name>
* kubectl rollout status deployment <deployment_name>
* kubectl rollout history deployment <deployment_name>
* kubectl rollout undo deployment <deployment_name>
* kubectl rollout undo deployment <deployment_name> --to-revision=<revision_number>
* kubectl autoscale deployment <deployment_name> --cpu-percent=50 --min=1 --max=10
* kubectl get hpa
* command to generate load : kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"
