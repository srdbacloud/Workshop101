First create a postgress database container called `db`, image `postgres`, environmental variable `POSTGRES_PASSWORD=mysecretpassword`

```
docker run --name db -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```


Next let's create a simple wordpress container called `wordpress`, image: `wordpress`, link it to the container `db` and expose it on host port `8085`
```
docker run -d --name=wordpress --link db:db -p 8085:80 wordpress
```


Storage: 


Run a  `mysql`  container named  `mysql-db`  using the  `mysql`  image. Set database password to  `db_pass123`

Note: Remember to run it in the detached mode
```
docker run -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
```
TO get data from saved in db  docker

```
docker exec mysql-db mysql -db_pass123 -e 'use db_name; slect * from table_name'
````



Run a mysql container again, but this time map a volume to the container so that the data stored by the container is stored at  `/opt/data`  on the host. Use the same name :  `mysql-db`  and same password:  `db_pass123`  as before. Mysql stores data at  `/var/lib/mysql`  inside the container.



```
`docker run -v /opt/data:/var/lib/mysql -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql`.
```
Now

Disaster strikes.. again! And the database crashed again. But this time we have the data stored at  `/opt/data`  directory. Re-deploy a new mysql instance using the same options as before.

Just run the same command as before. Here it is for your convinience: 
```
 docker run -v /opt/data:/var/lib/mysql -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
 ```

Networking:

View Networks in 

```docker network ls```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA1MzQ4MzA2MiwxNzc0MzYzMTY1XX0=
-->