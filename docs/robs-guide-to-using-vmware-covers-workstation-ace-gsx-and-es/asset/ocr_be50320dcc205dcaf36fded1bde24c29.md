To create a virtual machine, perform the following steps:

+   1. In your Farms view, select the GSX Server or ESX Server where you want to create the new virtual machine. Right click the host and select New virtual machine or select New virtual machine from the File menu.
+   2. In the virtual machine wizard, select a typical or custom method. For this example, I have decided to use the custom method.
+   3. Next, select where to place the virtual machine in VirtualCenter. Virtual machines can be grouped together; for example based on operating system, location, department, etc.

![](bbox=[0.12, 0.38, 0.62, 0.68])

Figure 42.5: VMs can be grouped to keep your VirtualCenter environment organized.

+   4. Select which operating system you will be installing inside this virtual machine.
+   5. Enter a name for your virtual machine and select the VMFS datastore that you want to store the virtual disk files (ESX) to, or the datastore that you have defined for your GSX Server that you want to store the machine's files to.
+   6. Select the number of processors to be used in this virtual machine. This is only available if you are configuring the machine for an ESX Server that has Virtual SMP installed.
+   7. Assign memory to the virtual machine.
+   8. Select the type of network for the virtual machine.