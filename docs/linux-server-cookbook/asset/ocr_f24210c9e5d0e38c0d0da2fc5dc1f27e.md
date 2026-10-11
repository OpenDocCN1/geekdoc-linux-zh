```
[root@server buildahexample]# buildah build -t ubuntuapache2:0.2 .
STEP 1/6: FROM ubuntu:latest
STEP 2/6: RUN apt-get update>/dev/null &&  apt-get install -y apache2 >/dev/null
debconf: delaying package configuration, since apt-utils is not installed
STEP 3/6: RUN echo "Image generated" > /var/www/html/index.html
STEP 4/6: COPY test.html /var/www/html/test.html
STEP 5/6: EXPOSE 80
STEP 6/6: CMD /usr/sbin/apache2ctl -D FOREGROUND
COMMIT ubuntuapache2:0.2
Getting image source signatures
Copying blob f4a670ac65b6 skipped: already exists
Copying blob 39f73f3d6bd1 done
Copying config 7efad98509 done
Writing manifest to image destination
Storing signatures
--> 7efad98509c
Successfully tagged localhost/ubuntuapache2:0.2
7efad98509cf7729d8b8a0d9668f3cea8a881c1555008f40e7030639bbe d1f1b
```

*Figure 13.49: Example using command buildah*

The tool **skopeo** allows to manipulate, inspect, sign, and transfer container images between different repositories. *Figure 13.50* shows how to use **skopeo** to inspect an image located in a repository:

```
[root@server ~]# skopeo inspect docker://docker.io/linuxservercb/ubuntuapache:latest
{
  "Name": "docker.io/linuxservercb/ubuntuapache",
  "Digest": "sha256:58557aced96f8d93717829e2ba6418e15ea0992e4c83c8659f6f21cead26381",
  "RepoTags": [
    "latest"
  ],
  "Created": "2022-11-01T21:27:15.186242452G",
  "DockerVersion": "20.10.21",
  "Labels": null,
  "Architecture": "amd64",
  "Os": "Linux",
  "Layers": [
    "sha256:301a8b87471f8f53a31e9c7e7fed5001ead5cb8f95bc2911c1cd266e060698d7",
    "sha256:cea0e2bcb017bb08e2c992e1d18ed553cfffcc2f b361e2475b3918c37087e25c2",
    "sha256:ec49d2122720a942642eda30d278620e8261db7dce5878322e904540b23881",
    "sha256:76f631053f2eef7b53ca36a172d52ada5a172efb92a1ff244efe53a5031b1b9d9"
  ],
  "Env": [
    "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
  ]
}
```

*Figure 13.50: Example using command skopeo*

Another useful task using **skopeo** is to copy images between different repositories. It is useful in having a disconnected repository from some official one to be able to do installations on environments that do not have direct access to the internet. *Figure 13.51* shows an example to copy the image **ubuntu:latest** to a private repository: