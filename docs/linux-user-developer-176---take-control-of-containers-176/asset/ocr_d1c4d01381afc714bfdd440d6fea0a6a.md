# Feature

# Take control of containers

# RUN ENTERPRISE-LEVEL CONTAINERS WITH MESOSPHERE

This distributed system simplifies building and running applications over large architectures

DC/OS is a distributed operating system based on the Apache Mesos distributed systems kernel. It enables the management of multiple machines as if they were a single computer. It automates resource management, schedules process placement, facilitates inter-process communication, and simplifies the installation and management of distributed services. Its web interface and command-line interface facilitate remote management and monitoring of the cluster and its services.

Apache Mesos is the open source distributed systems kernel at the heart of the Mesosphere DC/OS. Mesos began as a research project at UC Berkeley, the birthplace of BSD UNIX. Inspired by Google's proprietary Borg system, the project's goal was to create an open source kernel that simplifies building and running distributed applications at a very large scale and treats the entire data center as a single giant supercomputer, while also maintaining an extensible architecture.

![](bbox=[0.38, 0.3, 0.91, 0.54])

Traditional monolithic schedulers maintain the complete state of the application and infrastructure underneath, while also performing workload placement logic. This architecture makes it very challenging to scale and even harder to introduce new features and capabilities. With a dual-level architecture, Mesos handles low-level infrastructure scheduling operations, while another layer on top (the framework) handles all the application-specific operations and logic.

![](bbox=[0.1, 0.63, 0.36, 0.75])

masters process orchestrates tasks that are run on Mesos agents. It receives resource reports from Mesos agents and distributes those resources to registered DC/OS services, such as Marathon or Spark. Mesos agent nodes run discrete Mesos tasks on behalf of a framework. Private agent nodes run the deployed apps and services through a non-routable network. Public agent nodes run DC/OS apps and services in a publicly accessible network.

![](bbox=[0.67, 0.63, 0.91, 0.74])

provisioning container images (AppC is coming soon, too). This means that you can use both the Mesos containeriser and other container image types in DC/OS. You can also use the Docker container runtime directly with DC/OS, but the Universal container runtime supports running Docker images without depending on the Docker Engine, which allows for better integration with Mesos.

# 01 Architecture

The DC/OS kernel space is comprised of Mesos masters and Mesos agents. The user space includes system components such as Mesos-DNS, Distributed DNS Proxy, and services such as Marathon and Spark. The user space also includes processes that are managed by the services, for example a Marathon application. The Mesos

# 02 Mesos containerisers

Containerisers allow you to run tasks in containers. DC/OS supports two containeriser types – the DC/OS Universal container runtime and Docker containeriser. The Universal container runtime extends the Mesos containeriser to support