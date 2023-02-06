# DATABASE IN DOCKER

## MSYQSL

### Starting Your MySQL Container

Starting a MySQL container for the first time will automatically create an initial `root` user. You need to either supply a password for this user or ask MySQL to generate one. Here’s an example of running a basic MySQL container with a specified root password:

Start mysql container for the first

```
docker run --name mysql -d \
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD=change-me \
    --restart unless-stopped \
    mysql:latest
```

Access database inside the container

```
docker exec -it mysql mysql -p
```

OR

```
docker exec -it mysql mysql -h 127.0.0.1 -p
````

Persisting Data With Volumes

MySQL Docker image is configured to store all its data in the /var/lib/mysql directory. Mounting a volume to this directory will enable persistent data storage that outlives any single container instance.

Stop and remove your earlier container to avoid naming conflicts:

```
docker stop mysql
docker rm mysql
```

Then start a new container with the revised configuration:

```
docker run --name mysql -d \
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD=change-me \
    -v mysql:/var/lib/mysql \
    mysql:8
```

OR

```
docker run --name mysql -d \
    -p 3306:3306 \
    -e MYSQL_ROOT_PASSWORD=change-me \
    --restart unless-stopped \
    --tmpfs /var/lib/mysql \
    mysql:latest
```

Repeat the steps to stop and remove your container:

```
docker stop mysql
docker rm mysql
```

#### For more details and advance configuration visit [HERE](https://earthly.dev/blog/docker-mysql/)