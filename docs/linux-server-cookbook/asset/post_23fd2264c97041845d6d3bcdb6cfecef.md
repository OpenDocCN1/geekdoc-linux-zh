
of the applications can be performed on the *Public Cloud* when the tests and the required approvals are performed.
The *Public Cloud Providers* offer the possibility of communicating between both environments through a secure and private connection. *Figure 16.2* features a Hybride Cloud diagram:

![](img/863afa537de4eed7deb11978bfbfa90e_557_0.png)

## OpenStack as an IaaS

In the previous chapter, an introduction to **OpenStack** was described, including a list of the core components and other useful ones. This section will cover the architecture of **OpenStack**, its main use cases, and its advantages compared to a *Public Cloud*.

In an **OpenStack** cluster, there are two main types of nodes providing computing services:

- **Controller nodes**: They are servers running the database, queue services, load balancers, and **OpenStack** services accessible via *API*. These nodes include networking and storage services.
- **Compute nodes:** They run *Virtual Machines*, and they are responsible for the correct functioning.

Other types can be part of the cluster depending on the use case and the needs, for example:

- **Block storage nodes:** Nodes responsible for the storage, called *Volumes*, to be used by the *Virtual Machines*.
- **Object storage nodes:** Nodes responsible for the objects; it stores the *images* to be used by *Virtual Machines* and other unstructured data.

*Figure 16.3* represents an architecture example for **OpenStack**. It includes the core (controllers and compute) nodes and optional ones (Block and Object storage). Please refer to the following figure:

![](img/863afa537de4eed7deb11978bfbfa90e_559_0.png)

Figure 16.3: OpenStack architecture

The Networking configuration on OpenStack can be simple for development or proof of concept clusters or complex when the cluster is for production purposes. There are the following six main networks required in a production-ready installation when network isolation is used:

- **Control Plane** (also known as Provisioning): Used in development or installations without network isolation as the only one network. In a production-ready environment, this network is used for provisioning and management.
- **Internal API:** Communication to the *Services API* between the services. For example, the **nova** service (responsible for computing) communicates with the **neutron** service (responsible for networking) using this network.
- **Tenant:** Used by the *Virtual Machines* in the east-west traffic (communication between *Virtual Machines*) and the north-south traffic (from or to outside the *cluster*).
- **Storage:** Traffic generated from and to the systems providing the storage to **OpenStack**.
- **Storage Management:** Traffic used internally between the systems involved in the *Storage* systems.
- **External:** Used to provide external access from outside the cluster. The *Network* is used to provide an external address to be used for *API*, *Web access*, and access to the instances running on **OpenStack**.

An additional network called **Management** can be configured to access the cluster nodes to be administrated, usually only accessible by the teams who administrate the cluster. *Figure 16.4* shows a network layout for **OpenStack**:

![](img/863afa537de4eed7deb11978bfbfa90e_561_0.png)

Figure 16.4: OpenStack Network Layout. Source: Red Hat

Installation of **OpenStack** is a complex process, but there are available installation tools available, making the process easier. The two popular main options are as follows:

- **TripleO (OpenStack On OpenStack):** This project aims at the installation, upgrading, scaling, and operating **OpenStack**. The installation consists of a node called *undercloud*, which is an installation of **OpenStack** in a single node, which further helps the installation of an **OpenStack** cluster called *overcloud*. Figure 16.5 features a TripleO diagram:

![](img/863afa537de4eed7deb11978bfbfa90e_562_0.png)

- **OpenStack Charms**: This option uses **Metal-As-A-Service (MAAS)** and *Juju* projects. The project MAAS is used for provisioning a bare metal system, and *Juju* to deploy **OpenStack** services on the nodes.

**OpenStack** uses open-source projects to provide high availability of the services offered. The projects used to provide a reliable service are as follows:

- **Pacemaker**: A popular *High Availability* resource manager for *Linux*. It is responsible for ensuring that some of the services configured are available on the controller nodes. The services can be configured in active-passive or active-active. If it detects that some of the applications or nodes are not responding, it is responsible for promoting a node as active. The resources managed by *Pacemaker* are as follows:
    - *Gala*: A Multi-Master cluster for *MySQL/MariaDB* using synchronous replication.
    - *Haprox*: It is responsible for performing load balancing for the services offered by **OpenStack**.
    - *RabbitMQ, Qpid, or ZeroMQ*: The message queue service to coordinate operations and status information among services.
    - *Virtual IPs*: IP addresses associated with an application and move with the application when the application is moved from one server to another server. It allows a client to always call the same IP address instead of guessing where the application is running.
- **Memcached**: Used to cache tokens for the *Identity Service*.
- **Redis or MongoDB**: These NoSQL are used for the Telemetry Service.

The Controller nodes are usually three to guarantee the correct functionality of the system and provide high availability to the services. The number of Compute nodes depends on the resources for each of them and the needs of the end users. There are the following five main use cases for OpenStack these days:

- **Telco Companies**: These companies require a big performance and high bandwidth to offer telecommunication services to customers. OpenStack provides different options to increase performance, such as Real Time Kernel and Huge Pages. For data path networking, it is possible to use SRIOV or DPKD, among other solutions.
- **Service Providers**: These kinds of companies need the flexibility to create, scale, and delete services. OpenStack is a good solution to reduce operational costs.
- **Development**: Having a Private Cloud helps developers speed up the process and perform the testing.
- **Artificial Intelligence and Machine Learning (AI/ML)**: These technologies require access to special hardware to perform operations, such as a Graphical Process Unit (GPU). OpenStack is a perfect platform to run Virtual Machines to use virtual GPUs (vGPUS).
- **Edge Computing**: The current trend is to decentralize the infrastructure to have nodes to perform tasks in a different location. OpenStack allows it to be installed and contain Edge nodes.

## Running virtual machines on OpenStack

To operate with OpenStack, it is required to have the address to perform the authentication, a valid username, the password, and the project to be used. The authentication is performed against Keystone, which uses port 5000/tcp or 1300/tcp (TLS protected) to accept the requests. It is possible to specify the authentication data to the OpenStack command line client in the following three different ways:

- Using the file `clouds.yaml`, which can include different configurations for multiple installations. The environment variable `OS_CLOUD` or the option `--os-cloud` is used to specify the authentication to be used. This file can be located in the following directories, with the first having more priority:
    - Inside the current directory.
    - Inside the directory `~/.config/openstack`
    - Inside the directory `/etc/openstack`
- Using environment variables in the terminal to specify the values. Some variable examples are as follows:
    - `OS_AUTH_URL`: The *endpoint* URL against the client will perform the authentication.
    - `OS_PASSWORD`: The password for the specified username.
    - `OS_PROJECT_NAME`: The project name to be used during authentication.
    - `OS_USERNAME`: To specify the username to perform the authentication.
- Using the argument options for the client, some of them are as follows:
    - `--os-auth-url`: The *endpoint* URL against the client will perform the authentication.
    - `--os-password`: The password for the specified username.
    - `--os-project-name`: The project name to be used during authentication.
    - `--os-username`: To specify the username to be performed for the authentication.

The following block shows the example content of file `clouds.yaml` with two clusters configured:

```yaml
clouds:
  production:
    auth:
      auth_url: "https://production.osp.example.com:13000"
      username: "regularuser"
      project_name: "webproject"
      user_domain_name: "Default"
      password: "complexpassword"
      region_name: "regionOne"
      interface: "public"
      identity_api_version: 3
  developmnt:
    auth:
```
