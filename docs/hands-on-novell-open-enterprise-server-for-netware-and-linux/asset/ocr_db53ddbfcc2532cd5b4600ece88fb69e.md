# ## PREPARING FOR NetWARE 6.5 INSTALLATION

As described in Chapter 1, Novell's NetWare operating system has a long history of providing high-performance, reliable network services since the early 1980s. NetWare 6.5, the latest version of the NetWare kernel included in Novell's Open Enterprise Server distribution, continues to provide support for all Novell services and offers a wide range of development tools and utilities. Before performing a NetWare 6.5 Open Enterprise Server installation, you need to be prepared to supply information that the installation procedure requires and should be familiar with NetWare 6.5 hardware requirements and installation options. In this section, you learn the hardware requirements and the information for configuring the server and software components correctly.

# ### NetWare 6.5 Hardware Requirements

Essentially, NetWare 6.5 consists of an OS kernel (Server.exe) that provides core NetWare server services to the network and a software bus that allows other modules containing specialized services and control functions to be loaded and unloaded, as shown in Figure 2-1.

![](bbox=[0.08, 0.39, 0.95, 0.63])

**Figure 2-1**  NetWare 6.5 architecture

In addition to providing basic core NetWare services and support for loadable modules, the NetWare 6.5 kernel has been designed to support Java applications and provide Internet services using HTTP. These capabilities require additional system resources, such as processor speed and memory, that weren't needed in earlier NetWare versions. Because of its modular design, the hardware requirements needed to run NetWare 6.5 vary based on the number of modules and services to be loaded and the number of users logging in. The minimum hardware environment for installing a NetWare 6.5 server is shown in Table 2-1 along with the hardware recommended to satisfactorily support an average-size network environment.

**Table 2-1**  NetWare 6.5 hardware requirements

| Component | Minimum | Recommended |
| --- | --- | --- |
| Processor | Pentium II or AMD K7 | Pentium IV |
| Memory | 512 MB | 1 GB |