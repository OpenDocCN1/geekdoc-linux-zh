> exam Watch
> 
> To start and stop a VM, you can run the virsh start vmname and virsh destroy vmname commands, where vmname is the name of the VM, as shown in the output to the virsh list --all command.

Even on the most protected systems, power failures happen. Kernel updates still require a system reboot. In those cases, it's helpful to automate the start of VMs on a virtual host during the boot process.

In addition, the virsh command is the most straightforward way to make sure a VM is started the next time a system is booted. For example, the following command boots the noted tester1.example.com system during the

boot process of the host system.

```
# virsh autostart tester1.example.com
```

Once the boot process is complete for both the host and the VM, you'll be able to use commands like ssh to connect to that VM system normally. However, from the virtual host GUI, you'll still have to start the Virtual Machine Manager and connect to the associated hypervisor to actually connect to the virtual console for that tester1.example.com system.

The command creates a soft linked file in the /etc/libvirt/qemu/autostart directory. To reverse the process, either run the following command:

```
# virsh autostart --disable tester1.example.com
```

or delete the soft linked file named after the target VM from that directory.

# The virt-clone Command

The virt-clone --prompt command can be used to clone an existing VM. Before starting the process, make sure the system to be cloned is shut down. It's straightforward; one example where a tester1.example.com system is created from a server1.example.com system is shown in Figure 2-15.

> exam Watch
> 
> To configure a VM to start automatically when a system is booted, you can run the virsh autostart vmname command, where vmname is the name of the VM, as shown in the output to the virsh list --all command.

Once the process is complete, not only will you find the noted hard drive images in the

specified directories, but also you'll find a new XML configuration file for that VM in the /etc/libvirt/qemu directory.