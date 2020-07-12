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
````
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3Mjg0MjcwNzAsLTY5NDk4MTg5MF19
-->