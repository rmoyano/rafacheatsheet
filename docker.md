# Docker
Brief notes about Docker.

## Images
You can download images from [*DockerHub*](https://hub.docker.com/) or any other public registry:

Download the latest image:
```shell
user@notebook:~/code$ docker pull redis
Using default tag: latest
latest: Pulling from library/redis
faef57eae888: Pull complete 
bb595d48e52d: Pull complete 
d479b54c3bb2: Pull complete 
4bd00b511c2c: Pull complete 
286fb62a80b5: Pull complete 
520d4480047f: Pull complete 
Digest: sha256:1008c73f08e9f913868e2fa2e843212b62ea5bf3c66435d87bc7a6207bc0f1b4
Status: Downloaded newer image for redis:latest
docker.io/library/redis:latest
```
Download an specific version:
```shell
user@notebook:~/code$ docker pull redis:7.4.0
rmoyano@thinkpad:~$ docker pull redis:7.4.0
7.4.0: Pulling from library/redis
302e3ee49805: Pull complete 
5d0249d9189d: Pull complete 
4825c5e95815: Pull complete 
b0ce50685fa2: Pull complete 
455886c7d31b: Pull complete 
96377887d476: Pull complete 
4f4fb700ef54: Pull complete 
5fac73c23c9b: Pull complete 
Digest: sha256:6725a7dc7a44a6486b9d0a5172b10ccaf0c2ea600df87c0b93450d0e7769297f
Status: Downloaded newer image for redis:7.4.0
docker.io/library/redis:7.4.0

```

List images available in your system:
```shell
user@notebook:~/code$ docker images
REPOSITORY            TAG             IMAGE ID       CREATED        SIZE
ubuntu                latest          ba6acccedd29   2 months ago   72.8MB
dockercoins_webui     latest          df6098242320   4 months ago   218MB
redis                 latest          ddcca4b8a6f0   4 months ago   105MB
nginx                 latest          dd34e67e3371   4 months ago   133MB
python                alpine          d4d6be1b90ec   4 months ago   45.1MB
hello-world           latest          d1165f221234   10 months ago   13.3kB
python                3.6.8-stretch   48c06762acf0   2 years ago    924MB
```

If want to delete an image because it is not used anymore:
```shell
user@notebook:~/code$ docker rmi hello-world:latest 
Untagged: hello-world:latest
Untagged: hello-world@sha256:7d91b69e04a9029b99f3585aaaccae2baa80bcf318f4a5d2165a9898cd2dc0a1
Deleted: sha256:d1165f2212346b2bab48cb01c1e39ee8ad1be46b87873d9ca7a4e434980a7726
Deleted: sha256:f22b99068db93900abe17f7f5e09ec775c2826ecfe9db961fea68293744144bd
```


## Processes

Create a new container:
```shell
user@notebook:~/code$ docker create <CONTAINER_NAME> <image_name>
```

Start a container:
```shell
user@notebook:~/code$ docker start <CONTAINER_NAME>
```

Attach a container:
```shell
user@notebook:~/code$ docker attach <CONTAINER_NAME>
```

You can use *--attach* with run to execute both actions:
```shell
user@notebook:~/code$ docker run --attach <CONTAINER_NAME>
```

Stop a container:
```shell
user@notebook:~/code$ docker stop <CONTAINER_NAME>
```

Remove a container:
```shell
user@notebook:~/code$ docker rm <CONTAINER_NAME>
```

List Docker containers running:
```shell
user@notebook:~/code$ docker ps
CONTAINER ID   IMAGE                                 COMMAND                  CREATED        STATUS         PORTS                                NAMES
1e2c0835904e   gcr.io/k8s-minikube/kicbase:v0.0.39   "/usr/local/bin/entr…"   2 months ago   Up 9 seconds   127.0.0.1:32772->22/tcp, 127.0.0.1:32771->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32769->8443/tcp, 127.0.0.1:32768->32443/tcp   minikube-rmoyano-stx-env
```

List all the Docker containers (Running/Not running):
```shell
user@notebook:~/code$ docker ps -a
CONTAINER ID   IMAGE                                 COMMAND                  CREATED        STATUS                     PORTS                       NAMES
1e2c0835904e   gcr.io/k8s-minikube/kicbase:v0.0.39   "/usr/local/bin/entr…"   2 months ago   Up About a minute          127.0.0.1:32772->22/tcp, 127.0.0.1:32771->2376/tcp, 127.0.0.1:32770->5000/tcp, 127.0.0.1:32769->8443/tcp, 127.0.0.1:32768->32443/tcp   minikube-rmoyano-stx-env
1b5e235d82f3   ubuntu                                "bash"                   2 months ago   Exited (0) 2 months ago                                 sleepy_morse
8bd07cec6b82   hello-world                           "/hello"                 4 months ago   Exited (0) 2 minutes ago                                naughty_wiles
```