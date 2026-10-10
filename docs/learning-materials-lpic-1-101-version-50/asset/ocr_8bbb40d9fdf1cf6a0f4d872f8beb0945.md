and makes deploying a fleet of new systems on a cloud provider's platform easy.

The YAML file syntax used with `cloud-init` is called `cloud-config`. Here is a sample `cloud-config` file:

```
```css
#cloud-config
timezone: Africa/Dar_es_Salaam
hostname: test-system

# Update the system when it first boots up
apt_update: true
apt_upgrade: true

# Install the Nginx web server
packages:
 - nginx
```
```

Note that on the top line there is no space between the hash symbol (#) and the term `cloud-config`.

> NOTE `cloud-init` is not just for virtual machines. The `cloud-init` tool suite can also be used to pre-configure containers (such as LXD Linux containers) prior to deployment.

# ## Containers

Container technology is similar in some aspects to a virtual machine, where you get an isolated environment to easily deploy an application. Whereas with a virtual machine an entire computer is emulated, a container uses just enough software to run an application. In this way, there is far less overhead.

Containers allow for greater flexibility over that of a virtual machine. An application container can be migrated from one host to another, just as a virtual machine can be migrated from one hypervisor to another. However, sometimes a virtual machine will need to be powered off before it could be migrated, whereas with a container the application is always running while it is getting migrated. Containers also make it easy to deploy new versions of applications in tandem with an existing version. As users close their sessions with running containers, these containers can get automatically removed from the system by the container orchestration software and replaced with the new version thus reducing downtime.

> NOTE There are numerous container technologies available for Linux, such as Docker,