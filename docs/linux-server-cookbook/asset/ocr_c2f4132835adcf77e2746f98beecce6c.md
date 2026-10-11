needed, ensuring that it will not cause any interruption. This automation ensures if it detects any issue during the new configuration, a possibility to revert the changes will be there.

+   - **Resource provisioning:** Provisioning resources can involve to create new systems, such as virtual machines, virtual networks, or storage. The adoption of virtualization and containers converted this automation as essential.

+   - **Orchestration:** Modern infrastructures require multiple elements to be configured in parallel before reaching the desired status. Orchestration is responsible for coordinating and configuring the desired status inside the infrastructure.

+   - **Infrastructure as code:** A declarative definition of the desired infrastructure, where the automation tool will ensure to complete of all the needed tasks to accomplish the objective. Adoption of the Cloud popularized the tools using this approach.

Simple automation tools can be performed using shell scripting (also known as *bash scripting*) or using some popular programming language tool, such as *Python*. Linux offers multiple open-source, available tools for IT automation with different purposes:

+   - **Ansible:** The most popular general automation tool nowadays. Based on *playbooks* with *YAML* definition, it allows to automate of multiple elements, such as Linux and Windows systems, network devices, cloud infrastructures, and much more. One of the biggest advantages compared with other solutions is that it does not require an *agent* and uses protocols such as *SSH* and *WinRM* to administrate the systems.

+   - **Terraform:** One of the commonly used automation tools for *Infrastructure as Code*. It allows to create immutable infrastructure in different cloud and virtualization platforms.

+   - **Chef:** A configuration management and infrastructure automation tool based by default on an architecture server-client.

+   - **Puppet:** Configuration management with a declarative language to describe the desired system configuration, which requires a basic knowledge of programming.