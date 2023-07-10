# Docker
Brief notes about Docker.

## Images
You can download images from DockerHub or any other <reponame>:

List images available in your system:
```shell
user@debian:~/cheatsheet$ docker images
REPOSITORY            TAG             IMAGE ID       CREATED        SIZE
ubuntu                latest          ba6acccedd29   2 months ago   72.8MB
dockercoins_worker    latest          49c678e97107   4 months ago   54MB
dockercoins_webui     latest          df6098242320   4 months ago   218MB
redis                 latest          ddcca4b8a6f0   4 months ago   105MB
nginx                 latest          dd34e67e3371   4 months ago   133MB
python                alpine          d4d6be1b90ec   4 months ago   45.1MB
hello-world           latest          d1165f221234   10 months ago   13.3kB
python                3.6.8-stretch   48c06762acf0   2 years ago    924MB
```
If you want to delete an image because it is not used anymore:
```shell
user@debian:~/cheatsheet$ docker rmi hello-world:latest 
Untagged: hello-world:latest
Untagged: hello-world@sha256:7d91b69e04a9029b99f3585aaaccae2baa80bcf318f4a5d2165a9898cd2dc0a1
Deleted: sha256:d1165f2212346b2bab48cb01c1e39ee8ad1be46b87873d9ca7a4e434980a7726
Deleted: sha256:f22b99068db93900abe17f7f5e09ec775c2826ecfe9db961fea68293744144bd
```


## Processes

Create a new container:
```shell
user@debian:~/cheatsheet$ docker create <CONTAINER_NAME> <image_name>
```

Start a container:
```shell
user@debian:~/cheatsheet$ docker start <CONTAINER_NAME>
```

Attach a container:
```shell
user@debian:~/cheatsheet$ docker attach <CONTAINER_NAME>
```

You can use *--attach* with run to execute both actions:
```shell
user@debian:~/cheatsheet$ docker run --attach <CONTAINER_NAME>
```

Stop a container:
```shell
user@debian:~/cheatsheet$ docker stop <CONTAINER_NAME>
```

Remove a container:
```shell
user@debian:~/cheatsheet$ docker rm <CONTAINER_NAME>
```

List Docker containers running:
```shell
user@debian:~/cheatsheet$ docker ps
CONTAINER ID   IMAGE                                 COMMAND                  CREATED        STATUS         PORTS                                NAMES
1e2c0835904e   gcr.io/k8s-minikube/kicbase:v0.0.39   "/usr/local/bin/entr…"   2 months ago   Up 9 seconds   127.0.0.1:32772->22/tcp, 127.0.0.1:32771->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32769->8443/tcp, 127.0.0.1:32768->32443/tcp   minikube-rmoyano-stx-env
```

List all the Docker containers (Running/Not running):
```shell
user@debian:~/cheatsheet$ docker ps -a
CONTAINER ID   IMAGE                                 COMMAND                  CREATED        STATUS                     PORTS                       NAMES
1e2c0835904e   gcr.io/k8s-minikube/kicbase:v0.0.39   "/usr/local/bin/entr…"   2 months ago   Up About a minute          127.0.0.1:32772->22/tcp, 127.0.0.1:32771->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32769->8443/tcp, 127.0.0.1:32768->32443/tcp   minikube-rmoyano-stx-env
1b5e235d82f3   ubuntu                                "bash"                   2 months ago   Exited (0) 2 months ago                                 sleepy_morse
8bd07cec6b82   hello-world                           "/hello"                 4 months ago   Exited (0) 2 minutes ago                                naughty_wiles
```
