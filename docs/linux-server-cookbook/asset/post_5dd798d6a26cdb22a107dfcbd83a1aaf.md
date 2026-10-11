
Podman is an alternative to Docker that is getting popular on Red Hat Enterprise Linux systems and derivatives. The biggest difference between both is that Podman does not use a Daemon to run the containers. Each container is executed individually and is assigned to an individual systemd configuration. This allows the management of each container independently, and furthermore, containers will not be affected if the main Daemon is restarted or unexpectedly stopped, something which can happen in Docker.

Installing Podman in a system will replace Docker if it is installed and vice versa. Installation can be based on the Linux distribution repository, such as using apt or dnf commands. The command associated with Podman is called `podman`. This command has the same syntax as the `docker` command, with the exception of minor differences. The images to be used to run containers are the same as those used by Docker; these images use the format named Open Container Initiative (OCI). Figure 13.48 shows the argument run to create a new container.

```
[root@server ~]# podman run -dti -p 80:80 httpd
✓ docker.io/library/httpd:latest
Trying to pull docker.io/library/httpd:latest...
Getting image source signatures
Copying blob e559e5380898 done
Copying blob bc66ebea7efe done
Copying blob ee55cc448c8f done
Copying blob e9995326b091 done
Copying blob 5d0f831d3c0b done
Copying config fe8735c23e done
Writing manifest to image destination
Storing signatures
1668129b120866e8a0fc5bbc911195d6d9d52c8b89466d1ec2e7eb579fbd2de
```

Figure 13.48: Example running a container using podman

Podman solution comes with two commands for the Image building and for the Image distribution: `buildah` and `skopeo`. These need to be installed individually, and also included in the software repository. The first command uses the Dockerfile templates to build the destination Image and the second command is a powerful tool to operate with Images. Figure 13.49 shows the buildah command, using the same Dockerfile as previously for the docker build.

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

Figure 13.49: Example using command buildah

The tool **skopeo** allows to manipulate, inspect, sign, and transfer container images between different repositories. Figure 13.50 shows how to use **skopeo** to inspect an image located in a repository:

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

Figure 13.50: Example using command skopeo

Another useful task using **skopeo** is to copy images between different repositories. It is useful in having a disconnected repository from some official one to be able to do installations on environments that do not have direct access to the internet. Figure 13.51 shows an example to copy the image **ubuntu:latest** to a private repository:

```
[root@server ~]# skopeo copy docker://docker.io/ubuntu:latest \
> docker://registry.example.com:5000/ubuntu:latest \
> --dest-tls-verify=false
Getting image source signatures
Copying blob e96e057aae67 done
Copying config a8780b506f done
Writing manifest to image destination
Storing signatures
```

Figure 13.51: Example using command skopeo

## Container runtimes

As described previously, **Docker** and **Podman** are solutions to run containers on different platforms. Underneath, they are using a **Container Runtime** for that purpose. They are also responsible for network attachments, low-level storage, image transfer, and execution supervision.

There are different options available as follows:

- **runc**: A CLI tool for spawning and running containers on Linux, according to the OCI specification. This is the default one used by **Docker**.
- **crun**: A fast and low-memory footprint *OCI Container Runtime* fully written in C. This is the default one used by **Podman**.
- **Mirantis Container Runtime (MCR)**: Formerly called *Docker Engine—Enterprise*, it is a runtime supported by the company **Mirantis** after buying **Docker Enterprise**.

A **Container Runtime Interface (CRI)** is a plugin that allows **Kubernetes** to use a wide variety of **Container Runtimes**. The two main popular ones are as follows:

- **containerd**: This runtime is available as a daemon for Linux and Windows, which can manage the complete container life cycle of its host system.
- **CRI-O**: A lightweight container runtime for **Kubernetes**.

## Kubernetes

If **Docker** revolutionized the IT industry easing the container adoption and the modernization of the applications, **Kubernetes** went further and put the industry upside down in the way of working, deploying applications, and how the application modernization should be. **Kubernetes** offered container orchestration, whereas **Docker** tried with the project **Docker Swarm**. However, the limitations and the lack of functionalities converted **Kubernetes** into the perfect container orchestration solution.

**Kubernetes** provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, and more. Kubernetes provides the following:

- **Service discovery and load balancing**: Can expose a container using the DNS name or using their own IP address.
- **Storage orchestration**: Allows you to automatically mount a storage system of your choice, such as local storage, public cloud providers, and more.
- **Automated rollouts and rollbacks**: It is possible to describe the desired state for your deployed containers using **Kubernetes**, and it can change the actual state to the desired state at a controlled rate.
- **Automatic container distribution**: **Kubernetes** consists of a cluster of nodes that it can use to run containerized tasks. Each container defines how much CPU and memory (RAM) it needs. **Kubernetes** can fit containers onto your nodes to make the best use of your resources.
- **Self-healing**: **Kubernetes** restarts containers that fail, replaces containers, kills containers that do not respond to your user-defined health check, and does not advertise them to clients until they are ready to serve.
- **Secret and configuration management**: **Kubernetes** let you store and manage sensitive information, such as passwords, *OAuth tokens*, and *SSH keys*. You can deploy and update secrets and application configuration without rebuilding your container images and without exposing secrets in your stack configuration.

**Kubernetes** is a perfect platform for many use cases and enterprises of all sizes. But **Kubernetes** is not a **Platform-as-a-Service (PaaS)**, which includes all that is needed for the developers to build and run applications on it. In the market, *PaaS* solutions-based **Kubernetes** appeared, and it is distributed as *Kubernetes distributions*. The popular solutions are as follows:

- **Red Hat OpenShift Container Platform**: A full-stack automated operations and self-service provisioning for developers lets teams work together more efficiently to move ideas from development to production. The community-supported sibling project is named *OKD*.
- **Red Hat OpenShift Dedicated**: A managed Red Hat OpenShift offering on **Amazon Web Services (AWS)** and **Google Cloud**. Reduces operational complexity and focuses on building and scaling applications that add more value to your business with this turnkey application platform.
- **VMware Tanzu**: Provides a streamlined, self-service developer experience for any Kubernetes that fits a development team’s preferred practices and workflows while automating the toil of infrastructure, packaging, and security.
