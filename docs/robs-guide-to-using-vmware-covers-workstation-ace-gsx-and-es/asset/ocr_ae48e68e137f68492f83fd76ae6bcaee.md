# 5.2 Getting Started with VMware ACE

The software package that you work with as an administrator is called VMware ACE Manager. You will have to start out by installing this software to your workstation in order to create your ACE projects and to prepare the deployment to end users’ workstations.

Note: It is important to know that VMware ACE Administrator can not be installed in combination with other VMware products. Also, it is not possible to run existing virtual machines directly. The machines can be left intact, but you will always have to configure a VMware ACE project to point to the existing configuration. Therefore, if you want to keep using the VMware Workstation functionality as you are used to, you need to use a separate computer to manage your ACE environment (and no, you can not install the product inside a virtual machine). VMware ACE Manager does not interfere with VMware VirtualCenter and the remote console utilities for GSX Server and ESX Server.

Tip: If you need additional reading material on VMware ACE, you can check the online documentation. However, there are also a few very good resources available at the following URL:
www.vmware.com/support/resources/ace_resources.html.

Because you will not be using ACE Manager to run a large number of virtual machines at the same time, the hardware requirements are a little less. You can run multiple machines at the same time, but typically you just use one project with one machine at any given time. A PC with 1 GB of RAM should work well unless you are creating ACE workstations with larger amounts of RAM. For the client computers, it really depends on the machines you will be deploying and how much resources you need. However, for a typical Windows virtual machine with 256 MB of RAM which you want to run on a user’s computer, the user’s PC should have 512 MB of RAM.

Note: It is possible to use existing virtual machines from VMware Workstation version 4.5 in VMware ACE version 1.01, but VMs created with version 5 of VMware Workstation can not be used as VMware ACE machines.

Tip: If you already have a version 5 virtual machine which you want to use in VMware ACE, do the following: create a new virtual machine in version 5 and select to use legacy mode. Then use any of the physical to virtual conversion technologies described in this book to copy one machine to the other one. If you use a bootable Linux CD-ROM, you do not even have to buy any tools.

Most of the technical features of VMware ACE are identical to VMware Workstation. Some exceptions will be mentioned later in this chapter. But the hardware inside the virtual machines is the same and the list of guest operating systems is also very complete, and it is comparable to VMware Workstation version 4.5.