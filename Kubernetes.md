Kubernetes
-
```
kubectl get pods
```
```
kubectl describe pods
```
```
kubectl run nginx --image=nginx
```
```
kubectl get pods -o wide
```
```
kubectl describe pod newpod
```

How many containers are part of the pod 'webapp'?
```
kubectl describe pod webapp
```
Delete a POD
```
kubectl delete pod webapp
```
Create a new pod with the name 'redis' and with the image 'redis123'
```
kubectl run redis --image=redis123
```
Since redis123 is wrong image name editing it
```
kubectl edit pod redis
```


```
kubectl get replicaset
```
```
kubectl describe replicaset
```
TO find the correct version
```
kubectl explain replicaset|grep VERSION
```
Delete replicaset
```
kubectl delete replicaset
```
```
kubectl describe deployment'
```


For setting up your own network using flannel
```
kubectl create -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MjYwNjczMTVdfQ==
-->