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
If want to delete an image because it is not used anymore:
```shell
user@debian:~/cheatsheet$ docker rmi hello-world:latest 
Untagged: hello-world:latest
Untagged: hello-world@sha256:7d91b69e04a9029b99f3585aaaccae2baa80bcf318f4a5d2165a9898cd2dc0a1
Deleted: sha256:d1165f2212346b2bab48cb01c1e39ee8ad1be46b87873d9ca7a4e434980a7726
Deleted: sha256:f22b99068db93900abe17f7f5e09ec775c2826ecfe9db961fea68293744144bd
```


## Processes

Create a new Docker container:
```shell
user@debian:~/cheatsheet$ docker create <CONTAINER_NAME> <image_name>
```

To start a Docker container:
```shell
user@debian:~/cheatsheet$ docker start <CONTAINER_NAME>
```

To attach a Docker container:
```shell
user@debian:~/cheatsheet$ docker attach <CONTAINER_NAME>
```

You can use *--attach* with run to execute both actions:
```shell
user@debian:~/cheatsheet$ docker run --attach <CONTAINER_NAME>
```

To stop a Docker container:
```shell
user@debian:~/cheatsheet$ docker stop <CONTAINER_NAME>
```

To remove a Docker container:
```shell
user@debian:~/cheatsheet$ docker rm <CONTAINER_NAME>
```

To view Docker containers running:
```shell
user@debian:~/cheatsheet$ docker ps

```
To view all the Docker containers (Running/not running):
```shell
user@debian:~/cheatsheet$ docker ps -a


5. You can list all the branches created by using:
```shell
user@debian:~/gitnotes$ git branch -a
  feature1
* feature2
  main
  remotes/origin/HEAD -> origin/main
  remotes/origin/main
```
6. After you completed a feature, it's a good practice to delete that branch:
```shell
user@debian:~/gitnotes$ git branch -d feature2
Deleted branch feature2 (was f0d44a7).
```