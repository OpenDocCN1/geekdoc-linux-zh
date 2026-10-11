
## Conclusion

These days, **Containers** have become the main technology in the IT industry. It is important for System Administrators, Developers, and *DevOps* to have deep knowledge about the technology behind it and how to work with it. **Docker** and **Podman** help end user to run containers, create images, and perform **Continuous Integration**. Architectures that require multiple containers, microservices, and advanced features would require having knowledge about **Kubernetes**, and if a *Platform-as-a-Service* is required, they will be required to choose a solution based on **Kubernetes**, such as **Red Hat OpenShift Container Platform**.

**Continuous Integration** and **Continuous Delivery** are the main approaches to accelerate the software development process, reduce bugs, and help the collaboration between developers in the same team. Different open-source tools are available and combined with cloud-based solutions, and it is the decision of the team to choose the proper one for their own needs.

### Key facts

- **Containers** are not a new technology, but **Docker** popularized them.
- **Docker** is not a technology itself, but it is a high-level suite to run **Containers**.
- **Docker** is a client-service architecture; **Podman** does not require a server to run the containers.
- It is possible to have an internal (private) **Image Registry** to store the images generated.
- Different tools are available to perform **Continuous Integration**, and **Jenkins** is one of the most used.

### Questions

1. A **container** uses less resources than a **Virtual Machine**. True or false?
   - a. True
   - b. False
2. An **image** can only be used by one **container** at the same time. True or false?
   - a. True
   - b. False
3. What argument for the command **docker** is used to create a container without executing it?
   - a. create
   - b. run
   - c. add
4. Which command part of the **Podman** suite is used to build images?
   - a. buildman
   - b. buildar
   - c. buildah
5. What is the default name for a declarative **Pipeline** on **Jenkins**?
   - a. Pipefile
   - b. Jenkinsfile
   - c. Workflowile

### Answers

1. a
2. b
3. a
4. c
5. b

# CHAPTER 14

## Backup and Restore

### Introduction

Backup is the process of creating a copy of the data at a certain time with the objective of being able to recover it in the future. Restore is the process of recovering the data from a Backup, going back to an old version of the data, or reinstating a missing one. Backup requires a good definition, as well as planning and regular tasks to ensure the integrity of the copies.

This chapter covers the different strategies available for Backup and how it affects Restore. The storage media where Backup can be stored is discussed, as well as the different locations to protect the copies from possible disasters. Backup Solutions include different features to optimize the process, reducing the size stored with compression and removing duplicates, among other features. Two popular software detailed in this chapter are Bacula and Relax and Recover (ReaR).

### Structure

In this chapter, we will discuss the following topics:

- Introduction to backup and restore
- Storage media for backups
- Backup types
- Backup sources
- Backup strategies
- Backup solution features
- Bacula
- Relax-and-recover (ReaR)

### Introduction to backup and restore

The **Backup** process, and with it the **Restore** process, has evolved along with the big transformation in the **IT sector**. Big enterprises have dedicated teams to configure the target environment and the clients and are responsible for the planning as well. Good **Backup** planning is essential to avoid data loss, accelerate the recovery time, and perform tasks periodically to ensure the **Restore** is viable.

A **Backup** strategy requires the definition of the following factors:

- **The data to be included**: This is an important decision to take for many reasons, such as the size that the **Backup** will need, as well as the **Restore** time needed. For example, a **Backup** can include all the files from a system or only the files needed to reinstate after the system is reinstalled with a fresh *Operating System* installation.
- **The frequency**: It is important to define how often the **Backup** is going to be performed. The planning should include per environment frequency to be daily, weekly, monthly, or another specified period.
- **Backup method to use**: There are several methods to make copies, which are going to be explored in this chapter. This includes a **Full**, **Differential**, or **Incremental Backup**, among others.
- **The window-time for backups**: A **Backup** can be a long-time process, especially for **Full** ones, and can consume resources and network bandwidth. Deciding the window time to perform is one factor to be included in the planning.
- **Backup storage media**: A Backup usually generates several copies to protect against disaster scenarios. Different media can be used to store, such as *Tape*, *Shared Storage*, or *Cloud Storage*.
- **Retention**: **Backup** planning should define the retention of the data, and after that period, the copies would be removed to save space in the storage media.

For the **Restore**, the important factors in defining the recovery are as follows:

- **How Restore will be performed**: A **Backup** can include all the data required to restore a system or only those required for a service offered.
