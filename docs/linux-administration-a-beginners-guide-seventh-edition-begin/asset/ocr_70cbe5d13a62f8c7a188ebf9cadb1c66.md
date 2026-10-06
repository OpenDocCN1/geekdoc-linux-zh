# Using Docker Images

Docker images are the “bits and bobs” that make up containers. You will find thousands of images created by various projects, organizations, and individuals in the official Docker public registry. The registry stores images that are built for various uses, ranging from entertainment/multimedia uses, development environments, and various network servers (HTTP, DNS, VoIP, database and so on), all the way to complete operating systems that have been packaged into containers.

We will walk through setting up a container using a Docker image created by the official Apache Server Project (http://http.apache.org/).

+   1. Query your local Docker Host for existing images:

```
[root@fedora-server ~]# # docker images
```

The listing should be empty on a new Docker Host/installation.

+   2. Search the public Docker registry for images that have the keyword httpd

```
[root@fedora-server ~]# docker search httpd
```

The output should display available images. The NAME and OFFICIAL columns provides hints as to whether the image was uploaded by the official project maintainers or by individuals. The value in the STARS columns hints at the popularity of the image.

+   3. On our sample system, we will select and pull down the httpd image from the official source (NAME = docker.io/httpd), which also happens to be the one with the highest rating. Type

```
[root@fedora-server ~]# docker pull httpd
```

```
latest: Pulling from docker.io/httpd
1fb66afd9d0: Downloading [===== ] 16.24 MB/51.36 MB
```

+   4. Query your local image repository to list available images on your system:

```
[root@fedora-server ~]# docker images
```

| REPOSITORY TAG IMAGE ID CREATED VIRTUAL SIZE |
| docker.io/httpd latest de979434 two weeks ago 161.8 MB |

# Using Docker Containers

We downloaded the official httpd image in the previous section. The image is not terribly useful in its current form as it is just a bunch of files on our file system.