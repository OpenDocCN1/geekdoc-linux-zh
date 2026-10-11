An **Image** can be generated locally and stored in the system where the **container** will be executed. But the purpose of **Images** is to be used by **Containers** in different environments and systems. An **Image Registry** is a repository to store the **Images** to be used. This **Registry** can be a public one or a private one inside the infrastructure where it will be used.

When a **Container** is created, it refers to an **Image**, and if it is not downloaded previously, it will be automatically pulled from the **Image Registry**. Some popular public repositories are as follows:

+   - **Docker Hub**: The most popular repository. When **Docker** became popular, it was the main repository for public images to be used.

+   - **Quay**: A open-source repository with the possibility to deploy as on-promise.

An **Image Registry** enables users to build, organize, distribute and deploy containers. *Figure 13.4* shows an example workflow where the developer builds an **Image** and publishes it to an **Image Registry**. After the automatic tests are passed, they can be released to production to be used by the end users.

![](bbox=[0.2, 0.43, 0.8, 0.7])

# Docker

The project **Docker** was a revolution in the IT Industry because it made it easier to implement **Containers**. Traditionally, **Virtualization** was a fresh air of change for the companies to reduce costs and complexity in their infrastructures. However, it did not solve all the problems related to the development of the applications and the systems that were deployed. The introduction of the **Containers** in the development life-cycle helped *Developers* to be able to perform their tasks without the need for the creation of specific environments. Using the solution provided by **Docker**, they were able to use