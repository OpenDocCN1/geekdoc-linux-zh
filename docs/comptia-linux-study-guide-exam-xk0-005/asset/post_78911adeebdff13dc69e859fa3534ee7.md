
## EXERCISE 28.1 (*continued*)

The output shows that indeed the httpd container is running and that it has exposed the TCP 80 port on the container to TCP port 8088 on the host system.

- 5. Connect to the Apache web server running in the container by opening the browser in your host Linux desktop and typing **http://localhost:8088**. You will see the generic “It works!” message produced by the Apache web server.
- 6. Open an interactive Bash shell in the running container by typing `sudo docker exec -i -t myApache bash`. This connects to the container named myApache as an interactive terminal (the `-i` and `-t` options) and runs the bash command-line command, producing a shell prompt. You should see something like this:

```bash
$ sudo docker exec -it myApache bash
Emulate Docker CLI using podman. Create /etc/containers/nodocker to quiet msg.
root@43ee094b028d:/usr/local/apache2#
```

- 7. The Bash shell command prompt indicates that you are logged into the container OS as the root user account and that it is in the `/usr/local/apache2` directory. From there you can view and modify the Apache web server configuration files or create new web pages in the `/usr/local/apache2/htdocs` directory. To return to the host system command line, type **exit**.

```bash
root@43ee094b028d:/usr/local/apache2# exit
exit
[rich@localhost ~]$
```

- 8. Stop the running container by typing **sudo docker stop myApache**. You can verify that the container has stopped by typing **sudo docker ps**.
- 9. Delete the container from your Docker system by typing **sudo docker rm myApache**.
- 10. If you don’t want the httpd container image on your workstation anymore, type **sudo docker rmi httpd**.

## Summary

Cloud computing provides an easy way to expand the computing resources for a company without having to purchase and administer your own hardware. There are three levels of cloud computing that each provide different services. Infrastructure as a service (IaaS) provides hardware resources such as servers, storage, and network. Platform as a service (PaaS) provides development environments that consist of an operating system and any libraries required to develop, test, and deliver application software. Software as a service (SaaS) runs applications from the cloud servers across the Internet.

Cloud computing environments use virtualization to implement many servers without lots of physical hardware. With virtualization, one large server can host multiple smaller guest systems. The hypervisor software manages the resources allocated to each guest system and manages how those resources are used.

There are two types of hypervisor environments used. Type I hypervisors interact directly with the system hardware. Guest systems receive system resources directly from the hypervisor software. Type II hypervisors run on top of a host operating system. The host operating system interacts with the system hardware and provides resources to the Type II hypervisor, which in turn allocates the resources to the guest systems.

Containers are a different type of virtualization. Containers provide a consistent runtime environment for a single application. When you deploy an application into a container, the application container is guaranteed to run the same way no matter what server it runs on. By deploying applications using containers, you’re guaranteed the application will run the same way in the development, test, and production environments. Containers don’t contain as much overhead as virtual machines, making them easier to distribute.

## Exam Essentials

- **Describe the three primary methods of providing a cloud computing environment.** Public clouds are hosted on servers owned and operated by a third party. The company doesn’t own or operate any of the server hardware; it just utilizes space on those servers. Other companies can rent space in the same public cloud. Private clouds are hosted on servers located within the corporate network. All of the application files as well as data files reside within the corporate network. Hybrid clouds utilize private cloud servers but also interface them with public cloud servers. With the hybrid cloud, data could be located either externally in the public cloud or internally on the private cloud.
- **Explain the three types of cloud services.** Infrastructure as a service (IaaS) provides hardware-level services to customers. This includes servers, storage space, and the network resources to connect them. Platform as a service (PaaS) provides on-demand environments for developing software. In the PaaS cloud service, the server hardware, operating system, and runtime libraries are all provided by the cloud service. Software as a service (SaaS) runs applications in the cloud environment, allowing customers to access those applications via the Internet.
- **Explain the two types of hypervisors.** Type I hypervisors run directly on the system hardware. They act as a mediator between the hardware and the guest operating systems. Type I hypervisors allocate resources to each guest operating system, ensuring that each one gets enough. Type II hypervisors run on top of a host operating system. The host operating system interacts with the server hardware; the hypervisor software must go through the host operating system to access resources. Guest operating systems still only interact with the hypervisor software.
- **Describe how containers differ from virtual machines.** Most container packages don’t include a full operating system, but virtual machines do. Container packages only include the library files and application runtime files necessary to run a specific application. This makes the containers lightweight and easy to deploy.

## Review Questions

1. Which cloud service method utilizes only servers owned and operated by a third party?
    - A. Private
    - B. Public
    - C. Hybrid
    - D. Type II
    - E. Type I

2. Tom currently runs a cloud for his company on internal servers but needs some extra processing power to run a new application. What method of cloud service can he check out to leverage his existing cloud without needing to buy more internal servers?
    - A. Private
    - B. Public
    - C. Hybrid
    - D. Type I
    - E. Type II

3. Sally is interested in developing her application in the cloud without having to worry about administering an operating system. What type of cloud service should she buy?
    - A. PaaS
    - B. Private cloud
    - C. IaaS
    - D. SaaS
    - E. Hybrid cloud

4. Which type of cloud service allows you to spin up your own operating systems on infrastructure provided by the cloud?
    - A. PaaS
    - B. Private cloud
    - C. IaaS
    - D. SaaS
    - E. Hybrid cloud

5. Which type of hypervisor interfaces directly with the host system hardware?
    - A. Private
    - B. Public
    - C. Type II
    - D. Type I
    - E. Hybrid

6. Henry already has installed Red Hat Linux on his server but now needs to install virtual machines. What type of hypervisor package should he use?
    - A. Private
    - B. Public
    - C. Type II
    - D. Type I
    - E. Hybrid

7. Which type of hypervisor template bundles all of the configuration files into a single file for distribution?
    - A. XML
    - B. JSON
    - C. OVA
    - D. OVF
    - E. YAML

8. Fred wants to package his application so that it's guaranteed to run the same way no matter what Linux distribution his customers use. How can he do this?
    - A. Package the application as a container.
    - B. Package the application as a hypervisor.
    - C. Deploy the application to a private cloud.
    - D. Deploy the application as a virtual machine.
    - E. Bundle the application as a **tar** file and deploy it.

9. What method should you use to easily move an application from a development environment to a production environment without having to duplicate the operating system?
    - A. Public cloud
    - B. Private cloud
    - C. Type I hypervisor
    - D. Type II hypervisor
    - E. Container

10. Which Linux container package runs an engine as a process on the host operating system and provides a command-line interface to control containers?
    - A. Snap
    - B. Docker
    - C. KVM
    - D. XEN
    - E. VirtualBox
