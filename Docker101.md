Docker 
---
Installation: 
1. [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)
2.   If this is first time started to use docker head to last and choose Convenient Script ( Easy One ) if its Linux Kernel 

Unistall Any previous Version: 
```
sudo apt-get remove docker docker-engine docker.io containerd runc
```
Download the Script
```
curl -fsSL https://get.docker.com -o 
```
Run the Script
```
get-docker.sh
```
---
Basic Commands:

Run a Container: 
```
docker run nginx
```
ps - list containers
```
docker ps
docker ps -a
```
stop a container:
```
docker stop <container names>
```





<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2NTQzNTk4NTYsMTM4OTgxMDg3M119
-->