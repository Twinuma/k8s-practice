## Install
```
brew install kubectl
brew link --overwrite kubernetes-cli
kubectl version
```

## dashboard
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
kubectl get pod --namespace=kube-system -l k8s-app=kubernetes-dashboard
kubectl proxy
```

## Nodes
```
kubectl get nodes
```

## Namespace
```
kubectl get namespace
```

## Pod
```
kubectl apply -f simple-pod.yml
kubectl get pod

kubectl exec -it simple-echo sh -c nginx

kubectl logs -f simple-echo -c echo

kubectl delete pod simple-echo
kubectl delete -f simple-pod.yml
```

## ReplicaSet
```
kubectl apply -f simple-replicaset.yml
kubectl delete -f simple-replicaset.yml
```

## Deployment
```
kubectl apply -f simple-deployment.yml --record
kubectl get pod,replicaset,deployment --selector app=echo
kubectl rollout history deployment echo
kubectl get pod
kubectl get pod --selector app=echo
kubectl rollout history deployment echo --revision=1
kubectl rollout undo deployment echo
kubectl delete -f simple-deployment.yml
```

## Service
```
kubectl apply -f simple-replicaset-with-label.yml
kubectl get pod -l app=echo -l release=spring
kubectl get pod -l app=echo -l release=summner
kubectl run -i --rm --tty debug --image=gihyodocker/fundamental:0.1.0 --restart=Never -- bash -il
kubectl logs -f echo-summer-qvddt -c echo
kubectl get svc echo
```

## Ingress
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/provider/cloud-generic.yaml
kubectl -n ingress-nginx get service,pod
kubectl apply -f simple-service.yml
kubectl apply -f simple-ingress.yml
curl http://localhost -H 'Host: ch05.gihyo.local'
kubectl apply -f https://raw.githubusercontent.com/kubernetes/minikube/master/deploy/addons/freshpod/freshpod-rc.yaml
kubectl get pod -l app=nginx -w
```

## Job
```
kubectl apply -f simple-job.yml
kubectl logs -l app=pingpong
kubectl get pod -l app=pingpong --show-all
```

## CronJob
```
kubectl apply -f simple-cronjob.yml
kubectl get job -l app=pingpong
kubectl logs -l app=pingpong
```

## Secret
```
$ echo "hogefuga:$(openssl passwd -quiet -crypt whowho)" | base64
aG9nZWZ1Z2E6eXVGS0djYjlBQ2czTQo=

kubectl apply -f nginx-secret.yml
kubectl apply -f basic-auth.yml
```
