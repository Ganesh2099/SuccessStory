# SuccessStory

## Setup
```sh
alias k=kubectl
alias c=clear
alias h=history
complete -F __start_kubectl k
source <(kubectl completion bash)
export PS1="\e[0;32m \n\W > \e[0m"
```

# Commands :

```sh
kubectl api-resources
kubectl create -f <file_name>.yaml
kubectl apply -f <file_name>.yaml
kubectl apply -f ./my1.yaml -f ./my2.yaml
kubeadm token create --print-join-command    => to join worker node to master node
```

## Node

```sh
kubectl get nodes
kubectl describe node <nodename>
kubectl get nodes -o wide  
```

## Pod

```sh
kubectl run nginx-pod --image nginx
kubectl get pod
kubectl get pod -o wide
kubectl describe pod nginx-pod
kubectl logs nginx-pod
kubectl logs -f nginx-pod
kubectl get pod --show-labels
kubectl get pod -l tier=frontend
kubectl delete pod --all
kubectl exec -it nginx-pod -- bash
kubectl delete pod nginx-podd
kubectl run nginx-pod --image nginx --dry-run=client
kubectl run nginx-pod --image nginx --dry-run=client -o yaml
kubectl apply -f pod.yaml
kubectl delete -f pod.yaml
```

## Service

```sh
kubectl expose pod <pod_name> --type NodePort --port 80 --name frontend-service
kubectl expose pod <pod_name> --type LoadBalancer --port 80 --name frontend-service
kubectl expose pod <pod_name> --type ClusterIp --port 80 --name backend-service
kubectl get svc
kubectl describe svc <service_name>
minikube service <service_name> --url
k exec bz1 -- nslookup 192-168-41-151.default.pod
kubectl edit svc <service_name>
kubectl delete svc <service_name>
```

## ReplicaSet

```sh
kubectl apply -f rs_definition.yml
kubectl get replicaset
kubectl describe replicaset <replicaset_name>
kubectl edit replicaset <replicaset_name>
kubectl delete replicaset <replicaset_name>
```

## Deployment

```sh
kubectl apply -f deployment_definition.yml
kubectl apply -f deployment_definition.yml --record=true
kubectl get deployment
kubectl describe deployment <deployment_name>
kubectl edit deployment <deployment_name>
kubectl delete deployment <deployment_name>
kubectl rollout status deployment <deployment_name>
kubectl rollout history deployment <deployment_name>
kubectl rollout undo deployment <deployment_name>
kubectl rollout undo deployment <deployment_name> --to-revision=<revision_number>
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl autoscale deployment <deployment_name> --cpu-percent=50 --min=1 --max=10
kubectl get hpa

Note : Edit metrics server deployment with below to ignore ssl
    command:
    - /metrics-server
    - --kubelet-insecure-tls
```
  
## ConfigMap
```sh
kubectl create cm <cm_name> --from-literal city=pulgaon
kubectl create cm <cm_name> --from-env-file <file_name>
kubectl create cm <cm_name> --from-file <file_name>
kubectl create cm <cm_name> --from-file <file_name> --from-file <file_name>
kubectl create cm <cm_name> --from-file <dir_name>
kubectl create cm <cm_name> --from-literal city=pulgaon --dry-run=client -o yaml
kubectl get cm
kubectl describe cm <cm_name>
kubectl edit cm <cm_name>  
kubectl delete cm <cm_name>
```
  
## Secrets
```sh
kubectl create secret generic <secret_name> --from-literal city=pulgaon
kubectl create secret generic <secret_name> --from-env-file <file_name>
kubectl create secret generic <secret_name> --from-file <file_name>
kubectl create secret generic <secret_name> --from-file <file_name> --from-file <file_name>
kubectl create secret generic <secret_name> --from-file <dir_name>
kubectl create secret generic <secret_name> --from-literal city=pulgaon --dry-run=client -o yaml
kubectl get secret
kubectl describe secret <secret_name>
kubectl edit secret <secret_name>
aws ecr get-login OR docker login -u username -p password
kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username=subodhdere --docker-password=Docker@11 --docker-email=subodh.dere.7@gmail.com
kubectl delete secret <secret_name>
```

## Ingress
```sh
minikube addons enable ingress
kubectl get ingress
```

## ResourceQuota
```sh
kubectl get quota -n <namespace_name>
kubectl describe quota <ResourceQuota_name> -n <namespace_name>
kubectl describe quota <ResourceQuota_name> -n <namespace_name>
kubectl delete quota <ResourceQuota_name> -n <namespace_name>
```
  
## LimitRange
```sh
kubectl describe limits -n <namespace_name>
kubectl describe limits <LimitRange_name> -n <namespace_name>
kubectl describe limits <LimitRange_name> -n <namespace_name>
kubectl delete limits <LimitRange_name> -n <namespace_name>
```

## Namespace
```sh
kubectl get ns
kubectl describe ns <ns_name>
kubectl config set-context --current --namespace=sd
curl servicename.nsname.svc.cluster.local  => access service from different ns  
```
    
## Role
```sh
kubectl auth can-i delete pod -n test --as santosh
kubectl create role roledel -n test --verb delete --resource pod
kubectl get role
kubectl describe role <role_name>
kubectl delete role <role_name>
kubectl create rolebinding rb1 -n test --role roledel --user santosh  
kubectl get rolebinding
kubectl describe rolebinding <rolebinding_name>
kubectl delete rolebinding <rolebinding_name>
kubectl create clusterrole cr1 --verb list --resource pod
kubectl create clusterrolebinding crb1 --clusterrole cr1 --user santosh
```
  
## Config
```sh
openssl genrsa -out santosh.key 2048
openssl req -new -key santosh.key -out santosh.csr -subj "/CN=subodh/O=devops"
scp root@kmaster:/etc/kubernetes/pki/ca.{crt,key} .
openssl x509 -req -in subodh.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out subodh.crt -days 365
kubectl --kubeconfig subodh.kubeconfig config set-cluster kubernetes --server https://172.16.16.100:6443 --certificate-authority=ca.crt
kubectl --kubeconfig subodh.kubeconfig config set-credentials subodh --client-certificate subodh.crt --client-key subodh.key
kubectl --kubeconfig subodh.kubeconfig config set-context subodh-kubernetes --user subodh --cluster kubernetes
kubectl config use-context subodh-kubernetes --kubeconfig santosh.kubeconfig
kubectl auth can-i create pod -n test --kubeconfig subodh.kubeconfig
kubectl create role role1 -n test --verb create,list,delete --resource pod
kubectl create rolebinding rb1 -n test --role role1 --user subodh
kubectl get pod -n test --kubeconfig subodh.kubeconfig
```
        
## Scheduling
```sh
kubectl taint node minikube subodh=dere:NoSchedule|PreferNoSchedule|NoExecute
kubectl taint node minikube subodh=dere:NoSchedule-
```

## Job / Cronjob
```sh
kubectl create job job1 --image nginx
kubectl get job
kubectl describe job <job_name>
kubectl delete job <job_name>
kubectl get cj
kubectl describe cj <cj_name>
kubectl delete cj <cj_name>
```
