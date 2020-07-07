First create a postgress database container called `db`, image `postgres`, environmental variable `POSTGRES_PASSWORD=mysecretpassword`

```
docker run --name db -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```


Next let's create a simple wordpress container called `wordpress`, image: `wordpress`, link it to the container `db` and expose it on host port `8085`
```
docker run -d --name=wordpress --link db:db -p 8085:80 wordpress
```

Run a  `mysql`  container named  `mysql-db`  using the  `mysql`  image. Set database password to  `db_pass123`

Note: Remember to run it in the detached mode
```
docker run -d --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
```

sh get-data.sh

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY1Mzk5NzI3NCwtMTYzOTkxODY1NSwtMT
gwODcyODY4OF19
-->