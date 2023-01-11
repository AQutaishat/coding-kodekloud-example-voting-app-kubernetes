# kubernetes commands summery from udemy course 
URL: https://www.udemy.com/course/learn-kubernetes/

## Donwnloads: 
- kubectl
		https://kubernetes.io/docs/tasks/tools/
- minikube
		https://minikube.sigs.k8s.io/docs/start/
---

after installing minikube run
```Shell
minikube start --driver=hyperv 
```

```Shell
minikube servcie [service name] --url
```


## kubectl commands
```bash 
minikube status

kubectl get pods
kubectl get po
kubectl get replicaset
kubectl get rs
kubectl get deployments
kubectl get services

kubectl get pods -o wide
kubectl get services #get storage classes

kubectl run nginx --image=nginx
kubectl describe pod nginx
kubectl delete pod nginx

kubectl run radis --image=radis --dry-run=client -o yaml > radis.yaml # create yaml file automatically
kubectl create -f radis.yaml
kubectl apply -f radis.yaml

replication controller <===> replica set 

kubectl replace -f replicaset-definition.yml #to apply changes after editing the file
kubectl edit replicaset myapp-replicaset --record=true #to edit yamel and apply changes , even if the object does not have acutal yamel. record is to set label for the rollout in deployment
kubectl scale --replicas=6 -f replicaset-definition.yml #will not change number of replica in the file
kubectl scale --replicas=6 replicaset myapp-replicaset
kubectl describe replicaset myapp-replicaset

kubectl explain replicaset

kubectl create deployment --help
kubectl create deployment httpd-frontend --image=httpd:2.4-alpine --replicas=3

 kubectl rollout status deployment/myapp-deployment
 kubectl rollout history deployment/myapp-deployment

 kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1 --record=true
 kubectl rollout undo deployment/myapp-deployment #it adds new revistion and remove the old revision that rolled back to
```
* you can delete by :
  * file  name using (-f)
  * object name (kubectl delete deployment [name])
  * by using labels by using (-l)
    * ``` kubectl delete deployments, services -l group=example

* you can combine several objects in one yamel file and separate them by (---)
* you can specify how k8 check if pod is working or not, in definition of pod, add (livenessProbe), 
* use pod property (imagePullPolicy) and set it to (Always) to make it pull the image when it is changed not to have to change image tag to enforce pulling it

 * deployment rollout strategy type : recreate OR rollingUpdate (default)
 * deployment creates new version automatically when updating yaml file or execute command. +
* images must be on hub, not local images

 * three types of services (networking)
 	- nodePort: expose pods to outside node, the type (loadBalanc) is similar but for cloud apps or when install load balancer, if exists in local it will act like nodePort, (port, taregetPort, nodePort). it acts like node balancer between nodes using random algorithm, you access it using node url plus service nodePort port , you can get its url using (minikube service [name] --url). if same pod are spanned accross mulitple , it can be accessed on all nodes same way, node ip + service port, nodePort can be used for single pod in single node, or multi pod in single node, or multi pod in multi node. nodePorts range only betwee ( 3000 - 3767)
 	- clusterIP: internal network between pods (port, targetPort) , it can be used by name, 
-----------------------------------------
## kubernetes structure

* deployment (roll out, update, status, history)
	* replication set (desired count)
		* pods
* serivce (newtork router)
-----------------------------------------
URLS:
* https://kubernetes.io/docs/concepts/
* https://labs.play-with-k8s.com/
* https://kodekloud.com/
* https://cr2.udemy.com/course/learn-kubernetes/learn/lecture/9703196#overview
* https://minikube.sigs.k8s.io/docs/start/
* https://github.com/kubernetes/minikube/releases
* https://kubernetes.io/docs/tutorials/hello-minikube/
* https://kubernetes.io/
* 
* Kubernetes for the Absolute Beginners - Hands-on


