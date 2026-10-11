
## Software

Linux is a well-known platform for running applications and services in enterprise environments. But Linux is not limited to servers; it is a key part of the Information Technology industry and its general areas, such as:

- Software
- Devices and Infrastructure
- Information Technology and Business Services
- Emerging Technologies
- Telecommunications Services

This area includes developing software for business or customer markets, such as internet applications, system software, databases, management, home entertainment, and so on. Historically speaking, there was a gap between developers and the system administrators, as well as between the developers and the environment where the applications are executed.

Modern development methodologies are based on the balance and relationship between the system administrators and the programmers. The concept of **DevOps** is a set of practices that combines software development (**Dev**) with IT Operations (**Ops**). It aims to improve the system development life cycle and provides continuous delivery with high software quality.

**DevOps** methodology is based on multiple tools, called *toolchains*, and is deployed by Linux in different stages. Some of these tools will be covered in this book. The following figure illustrates this:

![](img/863afa537de4eed7deb11978bfbfa90e_30_0.png)

- **Plan:** This stage is the definition of the activities required.
  - *Jira* is one of the most popular tools for this stage that can be executed on Linux. Some open-source alternatives are *Taiga* and *Kanboard*.
- **Create:** This stage includes the coding, building, and integration with the source repository as well as the continuous integration.
  - Some popular tools are as follows:
    - For coding, Integrated Development Environments (*IDEs*): *Vim, Emacs*, and *Visual Studio Code*.
    - For repository and packaging: JFrog Artifactory, Sonatype Nexus, Gitlab.
    - For building and continuous integration: *Maven, Jenkins*, and *Gitlab CI*.
- **Verify:** This stage ensures the quality of the software. Different tests are performed during this stage related to security, integration, and performance.
  - Some popular tools are as follows:
    - Testing tools: Selenium, Appium, Cypress, and JMeter.
    - Bug tracking: Bugzilla, Redmine, and Mantis BT.
    - Code review: Gerrit, Gitlab, and ReviewBoard.
    - Security: OWASP ZAP, OSSEC, and SonarQube.
- **Package:** After the verification stage, the release is ready to be deployed in a system with similar characteristics than production; this environment is called stage or preproduction.
  - Popular tools include Docker and other tools described in the Create stage.
- **Releasing:** This is one of the most important stages of DevOps methodology, and it includes the orchestration and the deployment of the software to production.
  - Container platforms: Docker and Kubernetes.
  - Popular continuous development tools: goCD and ArgoCD.
- **Configuring:** This stage includes infrastructure configuration and management and infrastructure as code tools.
  - Popular tools examples: Ansible, Puppet, and Terraform.
- **Monitoring:** This stage examines the performance monitoring and end-user experience for the applications.
  - Popular tools examples: Prometheus and Grafana, Elastic Search, Zabbix, and Nagios.

Companies are using Linux for developing and run software due to the reliability, customization, and performance offered by this system. Linux offers a secure environment to run critical and customer-facing applications.

## Devices and Infrastructure

Linux is not only limited to physical servers or virtual machines. Rather, it is present in every device type available, some examples of which are as follows:

- Tiny computers like the popular Raspberry PI
- Tablets, Chromebooks, and E-readers
- Televisions and streaming devices
- Routers and other network devices
- Supercomputers: the top 500 of which are using Linux

Enterprise infrastructure has undergone a great transformation during the last two decades. Devices for storage and networking, for example, were previously closed proprietary platforms in a monolithic implementation but have now moved to a modular, open implementation, virtualized, or containerized environment. The term *Software-defined Infrastructure* is the result of the transformation for compute, storage, and network resources. Linux played a key part in this transformation in deploying the services with the same, if not better, efficiency.

**Software-defined compute (SDC):** Also known as virtualization, it is when a compute function is virtualized and is abstracted from the hardware that is running it. A popular solution for virtualization is *KVM*.

- **Software-defined network (SDN):** A network architecture that makes the management of the network more flexible and easier, SDN centralizes the management by abstracting the control plane from the data plane. Controllers, the core element of SDN architecture, are run in a Linux system. Some popular solutions are *OpenvSwitch*, *OVN*, and *OpenDayLight*.
- **Software-defined storage (SDS):** An architecture to offer dynamic storage to the endpoints, independent of the underlying hardware available. Some popular solutions are *Ceph* and *FreeNAS*.

## Information Technology and Business Services

IT services include providers offering services and integration, such as consulting and information management. This area also includes data processing and outsourcing services, including automation services.

### Business services

Business services offered by IT companies have been transitioning from an implementation and maintenance stage to offering services and integration solutions. The concept of “as-a-service” is currently one of the most important ones in business services, especially with the adoption of cloud computing. There are three popular types offered “as-a-service”, where Linux is a key component:

- **Software as a Service (SaaS)**: This service offers applications where everything behind is managed by the provider. This includes everything related to storage, network, virtualization, server, operating system, and runtime. In this category, popular Web services for e-commerce, document sharing, and editing, or online editors are also included.
- **Platform as a Service (PaaS)**: This service offers the possibility of running your own applications on a platform fully managed by the provider. In this scenario, only the application and data is managed by the customer. The environment to build, test, and run applications are offered for that purpose. Some examples are OpenShift, Heroku, and PaaS, offered by cloud providers such as AWS Elastic Beanstalk, Google App Engine, or WindowsAzure.
- **Infrastructure as a Service (IaaS)**: This service offers the infrastructure required by the customer to provide solutions to end users. Networking, storage, servers, virtualization (if needed), operating system, and the rest of the elements needed to offer the solutions are managed by the administrator of the IaaS (the client who requested it). Popular private IaaS includes OpenStack, and popular public solutions include DigitalOcean, Rackspace, and services offered by public clouds such as AWS, Google Cloud, IBM Cloud, and Microsoft Azure, among others.

The following figure compares the three popular types, indicating the elements managed by the customer as well as the elements managed by the service provider:

![](img/863afa537de4eed7deb11978bfbfa90e_34_0.png)

*Figure 1.2: Differences between On-Site, IaaS, PaaS, and SaaS. Source: Red Hat*

### Automation services

Automation and integration services are key parts in the implementation of solutions. With automation solutions, companies can design and implement processes to reduce human interventions, including application release, providing new services, or scaling existing ones. Popular automation tools such as *Ansible* and *Terraform* are widely used to facilitate the orchestration and integration of new services.

## Emerging technologies
