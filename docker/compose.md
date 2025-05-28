# Docker Compose
Brief notes about [*Docker Compose*](https://docs.docker.com/compose/).

## Management

Create and start all the services from your configuration file:
```shell
user@notebook:~/code$ docker compose up
WARN[0000] /home/rmoyano/docker/docker-compose.yml: `version` is obsolete 
[+] Running 3/0
 ✔ Network docker_postgres_net    Created                                   0.0s 
 ✔ Volume "docker_postgres_data"  Create...                                 0.0s 
 ✔ Container test_postgres        Created                                   0.0s 
Attaching to test_postgres
test_postgres  | The files belonging to this database system will be owned by user "postgres".
test_postgres  | This user must also own the server process.
```
Create and start all the services from your configuration file, using detached mode:
```shell
user@notebook:~/code$ docker compose up -d
[+] Building 2.2s (11/11) FINISHED                                docker:default
 => [app internal] load build definition from Dockerfile                    0.0s
 => => transferring dockerfile: 300B                                        0.0s
 => WARN: ConsistentInstructionCasing: Command 'workdir' should match the   0.0s
 => [app internal] load metadata for docker.io/library/python:3.8-alpine    2.0s
 => [app internal] load .dockerignore                                       0.0s
 => => transferring context: 61B                                            0.0s
 => [app internal] load build context                                       0.0s
 => => transferring context: 179B                                           0.0s
 => [app 1/6] FROM docker.io/library/python:3.8-alpine@sha256:3d93b1f77efc  0.0s
 => CACHED [app 2/6] WORKDIR /storeapi                                      0.0s
 => CACHED [app 3/6] COPY requirements.txt .                                0.0s
 => CACHED [app 4/6] RUN pip install --upgrade pip &&     pip install -r r  0.0s
 => CACHED [app 5/6] COPY api/ api/                                         0.0s
 => CACHED [app 6/6] WORKDIR api                                            0.0s
 => [app] exporting to image                                                0.0s
 => => exporting layers                                                     0.0s
 => => writing image sha256:06aeeecd2a211f5bca08af94ff7b6e32a1562e7ca6820e  0.0s
 => => naming to docker.io/library/storeapi-app                             0.0s
[+] Running 2/2
 ✔ Container test-mongo  Started                                            0.4s 
 ✔ Container flask_app   Started   
```
To check what is currently running:
```shell
user@notebook:~/code$ docker compose ps
NAME         IMAGE          COMMAND                  SERVICE   CREATED         STATUS         PORTS
flask_app    storeapi-app   "python -m flask run…"   app       6 seconds ago   Up 5 seconds   0.0.0.0:5000->5000/tcp, :::5000->5000/tcp
test-mongo   mongo:5.0      "docker-entrypoint.s…"   mongo     6 seconds ago   Up 5 seconds   27017/tcp
```

Create and start all the services from your configuration file:
```shell
user@notebook:~/code$ docker compose logs
rmoyano@thinkpad:~/docker$ docker compose logs
WARN[0000] /home/rmoyano/docker/docker-compose.yml: `version` is obsolete 
test_postgres  | The files belonging to this database system will be owned by user "postgres".
test_postgres  | This user must also own the server process.
test_postgres  | 
test_postgres  | The database cluster will be initialized with locale "en_US.utf8".
test_postgres  | The default database encoding has accordingly been set to "UTF8".
test_postgres  | The default text search configuration will be set to "english".
test_postgres  | 
test_postgres  | Data page checksums are disabled.
test_postgres  | 2025-05-28 14:18:55.334 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
test_postgres  | 2025-05-28 14:18:55.342 UTC [55] LOG:  database system was shut down at 2025-05-28 14:18:55 UTC
test_postgres  | 2025-05-28 14:18:55.353 UTC [1] LOG:  database system is ready to accept connections
```

To stop the running services:
```shell
user@notebook:~/code$ docker compose stop
[+] Stopping 2/2
 ✔ Container flask_app   Stopped                                           10.3s 
 ✔ Container test-mongo  Stopped                                            0.3s 
```
To stop and remove the running services (Containers and networks):
```shell
user@notebook:~/code$ docker compose down
[+] Running 3/3
 ✔ Container flask_app       Removed                                       10.4s 
 ✔ Container test-mongo      Removed                                        0.3s 
 ✔ Network storeapi_backend  Removed                                        0.4s
```
To stop and remove all running services (Containers, networks and volumes):
```shell
user@notebook:~/code$ docker compose down -v
rmoyano@thinkpad:~/flaskapp/storeapi$ docker compose down -v
WARN[0000] /home/rmoyano/docker/docker-compose.yml: `version` is obsolete 
[+] Running 3/3
 ✔ Container test_postgres      Removed                                     0.3s 
 ✔ Volume docker_postgres_data  Removed                                     0.0s 
 ✔ Network docker_postgres_net  Removed                                     0.3s
```
----

## Compose file
Using Docker command to run Postgresql database with env vars, volumes and networks.

```shell
rmoyano@thinkpad:~/docker$ docker run -d --name test_postgres \
  --network test-net \
  -p 5432:5432 \
  -e POSTGRES_USER=rafa \
  -e POSTGRES_PASSWORD=admin \
  -e POSTGRES_DB=test_docker \
  -v postgres_data:/var/lib/postgresql/data \
  postgres:14-alpine
b24bd54f9ce9cde6210220733b3bfc2b03884fdb297a903f0c9764b224cc6163
docker: Error response from daemon: failed to set up container networking: network test-net not found

rmoyano@thinkpad:~/docker$ docker network list
NETWORK ID     NAME      DRIVER    SCOPE
a82898c025e0   bridge    bridge    local
9807d7124409   host      host      local
48c9e74aa4da   none      null      local
rmoyano@thinkpad:~/docker$ docker network create test-net
6a4830f05936993c6bb9870adcda1e9bcd5ea37d8640a2fc89b8c9e56e2054ef
rmoyano@thinkpad:~/docker$ docker network list
NETWORK ID     NAME       DRIVER    SCOPE
a82898c025e0   bridge     bridge    local
9807d7124409   host       host      local
48c9e74aa4da   none       null      local
6a4830f05936   test-net   bridge    local

$ docker run -d --name test_postgres \
  --network test-net \
  -p 5432:5432 \
  -e POSTGRES_USER=rafa \
  -e POSTGRES_PASSWORD=admin \
  -e POSTGRES_DB=test_docker \
  -v postgres_data:/var/lib/postgresql/data \
  postgres:14-alpine

rmoyano@thinkpad:~/docker$ docker network rm test-net 
test-net
```

Yaml file using Postgresql as example listing networks and volumes:
```yaml
services:
  test_postgres:
    image: postgres:14-alpine
    container_name: test_postgres
    environment:
      POSTGRES_USER: rafa
      POSTGRES_PASSWORD: admin
      POSTGRES_DB: test_docker
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - postgres_net
    restart: unless-stopped

volumes:
  postgres_data:

networks:
  postgres_net:
```

Start a container:
```shell
user@notebook:~/code$ docker-compose up
Creating test_postgres ... done
Attaching to test_postgres
test_postgres    | The files belonging to this database system will be owned by user "postgres".
test_postgres    | This user must also own the server process.
test_postgres    | 
test_postgres    | The database cluster will be initialized with locale "en_US.utf8".
test_postgres    | The default database encoding has accordingly been set to "UTF8".
test_postgres    | The default text search configuration will be set to "english".
test_postgres    | 
test_postgres    | Data page checksums are disabled.
test_postgres    | 
test_postgres    | fixing permissions on existing directory /var/lib/postgresql/data ... ok

test_postgres    | 2025-05-28 15:42:04.551 UTC [1] LOG:  database system is ready to accept connections
^CGracefully stopping... (press Ctrl+C again to force)
Stopping test_postgres ... done
```
