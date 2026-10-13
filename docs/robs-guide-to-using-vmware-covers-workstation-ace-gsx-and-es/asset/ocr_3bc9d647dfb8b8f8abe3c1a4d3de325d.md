Tip: If you notice strange heartbeat behavior, such as when the percentage is low but the virtual machine is actually performing very well by itself, check whether you have the correct version of VMware tools loaded inside the guest operating system.

# Adding a virtual machine

When you are at this point in the configuration, I expect that you have already created you first virtual machine. In the Management Interface, click the link for Add Virtual Machine and follow the instructions. I will not go into a lot of detail about creating virtual machines here. The information about virtual machines in the first part of this book regarding installation of Windows, Linux, and NetWare and the installation of the guest OS tools is identical for virtual machines that you create for your ESX Server. There are a few specific configurations that I would like to discuss, because they are ESX Server specific.

# Using multiple processors

This is one of the first additional configuration options which you will see when creating virtual machines. If you own a license for VMware's additional product Virtual SMP, then you can assign a maximum of two CPUs to the machine for the guest to use.

![](bbox=[0.08, 0.56, 0.68, 0.77])

When the virtual machine is created, regardless of whether you have the Virtual SMP product, if you have multiple processors, then you can configure which CPUs can be used by the virtual machine and which ones can not. This can be done from the CPU tab in the virtual machine configuration screen.

Figure 40.2: A virtual machine can be configured to run on specific processors.

# Adding virtual disk files

The next step in creating a virtual machine is to assign a virtual disk. You can choose to use an existing one or to create a new one. If you have a SAN, you can also assign physical LUNs to a virtual machine to be used.