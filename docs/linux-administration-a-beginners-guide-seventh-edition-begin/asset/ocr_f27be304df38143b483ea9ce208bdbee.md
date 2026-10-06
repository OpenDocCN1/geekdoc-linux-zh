# Linux Administration: A Beginner's Guide

To make the image useful, we have to spin up our very own container from it and customize that container for our own use.

+   Without further ado, let's fire up our httpd container:
```bash
[root@fedora-server ~]# docker run \
--net \
--name my-lst-container \
-p 80:80 \
docker.io/httpd
```nThe options we passed to the docker command are
* --net Specifies the type of networking that we want to use for the container. We've specified the host networking option.
* --name This is a descriptive name to assign to this container instance. We are using my-lst-container as the name in this example.
* --p (abbreviated form of --publish) Maps or publishes a container's port(s) to the host. Here we are mapping port 80 (default HTTP port) on the container to host port 80.
* -d (abbreviated form of --daemon) Runs the container in the background. This runs the container as a daemon.
* docker.io/httpd Specifies the image name. Here we are referring to the image that we downloaded earlier.

+   Query docker for the list of running containers:
```bash
[root@fedora-server ~]# docker ps
```

+   Once the container launches successfully, you can point your web browser to the IP address of the Docker Host to view the default/basic web page being served from the container or use any capable CLI program like curl or wget. IP address of our sample Docker Host is 192.168.1.100, so we'll use curl to browse the web server running in the container like:
```bash
[root@fedora-server ~]# curl http://192.168.1.100
```

> TIP The port that was mapped from the container to the host needs to be accessible through any host-based firewall rules. For this httpd container example, you'll need to open port 80 on the docker host. For Fedora, CentOS, or RHEL-based Linux distro, you can use the firewall-cmd to do this like so:
# firewall-cmd --permanent --add-service=http
# firewall-cmd --reload