# MongoDB docker service

1. change the password in `.env` file

2. start the service

```sh
docker-compose up -d
```

wait for it to initialize completely, and visit http://swarm-ip:8888, http://localhost:8888, or http://host-ip:8888 (as appropriate).

# Container shell access and viewing MongoDB logs

The docker exec command allows you to run commands inside a Docker container. The following command line will give you a bash shell inside your mongo container:

```sh
$ docker exec -it some-mongo bash
```
The MongoDB Server log is available through Docker's container log:

```sh
$ docker logs some-mongo
```

# Creating database dumps

Most of the normal tools will work, although their usage might be a little convoluted in some cases to ensure they have access to the mongod server. A simple way to ensure this is to use docker exec and run the tool from the same container, similar to the following:

```sh
$ docker exec some-mongo sh -c 'exec mongodump -d <database_name> --archive' > /some/path/on/your/host/all-collections.archive
```