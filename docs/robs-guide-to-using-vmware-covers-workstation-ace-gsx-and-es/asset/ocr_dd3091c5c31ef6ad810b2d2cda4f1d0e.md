# 42 Introduction to VirtualCenter

In a multi VMware server environment, with GSX Servers, ESX Servers, or in a mixed environment, the management can very easily become very complex. To manage virtual machines, you must access several Management Interfaces on individual hosts. Also, accessing virtual machine console requires access to several hosts with the Virtual Machine Console utility. And when multiple administrators need to have rights to servers, which of course will be different levels of rights, it requires a lot of work to configure all them on individual hosts.

To solve these manageability issues, VMware has created the VirtualCenter. With this application you can manage a mix of VMware GSX and ESX Servers. And it is also the platform that you must use when you want to use the vMotion application to perform transfers of virtual machines to other hosts.

Another important feature of VirtualCenter is that it helps you evaluate the load of your virtual machine environment. Within one central location, you can monitor what all the servers are doing, and when the problems occur, and you can take the right action. VirtualCenter even enables you to assign actions to typical events and warn you, for example when CPU load reaches a threshold. Last but not least, VirtualCenter supports easy deployment of new virtual machines based on templates.

Note: As was the case in chapter 1, which covered the ESX Server, this chapter is not a complete VirtualCenter manual. My intention is to get you started with the application in a clear and simple manner.

Before we get into the installation of the product itself, there is some terminology that you need to be familiar with.

# VirtualCenter Server

This is a Windows-based application that runs on a Windows Server platform. It is the central node in the entire VirtualCenter infrastructure. It communicates with the VirtualCenter agents on the hosts and the administrators attach to this server with their client application.

# VirtualCenter Client

This is the Windows based application that an administrator runs to manage the virtual machine environment. The client application communicates with the VirtualCenter server.

# VirtualCenter Agent

This is the software that runs on every VMware GSX Server and ESX Server. It collects the information that is sent to the VirtualCenter Server and it performs the actions that are sent by the server.