First create a postgress database container called `db`, image `postgres`, environmental variable `POSTGRES_PASSWORD=mysecretpassword`

```
docker run --name db -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```


Next let's create a simple wordpress container called `wordpress`, image: `wordpress`, link it to the container `db` and expose it on host port `8085`
```
docker run -d --name=wordpress --link db:db -p 8085:80 wordpress
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4MDg3Mjg2ODhdfQ==
-->