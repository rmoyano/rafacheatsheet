# VI/VIM

Brief notes about VI/VIM.

## Insert mode

|#  | Action        | Command       |
|---| ------------- |:-------------:|
|1| Insert mode | i |
|2| Delete character | x |
|3| Delete from current character to beginning of the line | d0 |
|4| Delete from current character to end of the line | d$ |
|5| Delete line | d |
|6| Delete 3 lines | 3d |
|7| Delete from current line to the top of the file | dgg |
|8| Delete from current line to the end of the file | dG |
|9| Replace character | r |
|10| Copy line| yy |
|11| Paste line below current | p |
|12| Paste line above current | Shift + p |
|13| Paste 3 times the copied line below current | 3p |
|14| Paste 3 times the copied line above current | 3P |
|15| Go to first line in file | 1G |
|16| Go to last line in file:  | G |
|17| Save file | ESC + :w |
|18| Exit file | ESC + :q |
|19| Save file and quit VI | ESC + :wq |
|20| Save file and quit VI | ESC + :x |
|21|  |  |

----

## Images
# Show special characters
You can download images from DockerHub or any other <reponame>:

```shell
:set list
:set nolist
```

If want to delete an image because it is not used anymore:
```shell
user@debian:~/cheatsheet$ docker rmi hello-world:latest 
Untagged: hello-world:latest
Untagged: hello-world@sha256:7d91b69e04a9029b99f3585aaaccae2baa80bcf318f4a5d2165a9898cd2dc0a1
Deleted: sha256:d1165f2212346b2bab48cb01c1e39ee8ad1be46b87873d9ca7a4e434980a7726
Deleted: sha256:f22b99068db93900abe17f7f5e09ec775c2826ecfe9db961fea68293744144bd
```