| WORKDIR | Sets the working directory inside the container. |
| ENV | Sets the environment variables inside the image. |
| ARG | Specifies the arguments which can be accepted using the option --build-args |
| HEALTHCHECK | Specifies health check tests to ensure the container is working properly. |

# *Table 13.2: Statements available in Dockerfile*

After the **Image** is generated, it is possible to publish it to a public registry, such as [https://hub.docker.com](https://hub.docker.com) or [https://www.quay.io](https://www.quay.io). It is possible to create a free account for personal usage and store-created images. Other plans for companies are available. After an account is created, it is possible to use the argument **login** from the command **docker** to perform a login before to publish the desired **Image**. *Figure 13.43* shows the login example to **Docker Hub**.

```
```
root@ubuntu:~# docker login docker.io
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: linuxservercb
Password:
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store
Login Succeeded
```
```

# *Figure 13.43: Example of logging into Docker Hub*

After the login succeeds, the **Image** needs to be *tagged* with the correct format for the desired repository. For **Docker Hub**, the format is **docker.io/USERNAME/name:image:tag**. After the **Image** has the correct name, the argument **publish** will upload and create the image in the repository. *Figure 13.44* shows the tagging and the publishing task:

```
```
root@ubuntu:~# docker tag ubuntuapache2:0.1 docker.io/linuxservercb/ubuntuapache
root@ubuntu:~# docker push docker.io/linuxservercb/ubuntuapache
Using default tag: latest
The push refers to repository [docker.io/linuxservercb/ubuntuapache]
ddf96998d2d7: Pushed
0ff7c267b89e: Pushed
bcebf94eb56: Pushed
7ea4455e747e: Mounted from library/ubuntu
latest: digest: sha256:58557aced96f8d9371782e92ba6e418e15ea0992e4c83c8659f6f21cee
d26381 size: 1155
```
```

# *Figure 13.44: Example of pushing an Image to Docker Hub*

After the image is published, the *image* is available in the **Docker Hub** portal. As the image did not specify any *image* tag, it is tagged locally and in the *registry* with the word *latest*. *Figure 13.45* shows the **Docker Hub** portal for the image published: