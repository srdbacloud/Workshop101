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
Since redis123 is wrong image name ed
```
kubectl edit pod redis
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg2NjkzNzE5OCwtMjA3MTc2OTU2MV19
-->