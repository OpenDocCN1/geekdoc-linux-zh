```
libvirt-lxc.so.0 => /lib64/libvirt-lxc.so.0 (0x00007f4a3a10c000)
libvirt-qemu.so.0 => /lib64/libvirt-qemu.so.0 (0x00007f4a39f08000)
libvirt.so.0 => /lib64/libvirt.so.0 (0x00007f4a39934000)
$
```

A primary goal of the `libvirt` project is to provide a single way to manage virtual machines. It supports a number of hypervisors, such as KVM, QEMU, Xen, and VMware ESXi. You can find out more about the `libvirt` project at the `Libvirt.org` website.

# ## Viewing `virsh`

One handy tool that uses the `libvirt` library is the `virsh` shell. It is a basic shell you can employ to manage your system’s virtual machines.

> NOTE
> If you’d like to try out the `virsh` shell, you can obtain it through the `libvirt-client` or `libvirt-clients` package. For older distributions, it may be located in the `libvirt-bin` package. Package installation was covered in Chapter 13, “Governing Software.” Be aware that additional software packages are needed to create virtual machines.

If you have a VMM (hypervisor) product installed, you can employ the `virsh` shell to create, remove, start, stop, and manage your virtual machines. An example of entering and exiting the `virsh` shell is shown in Listing 29.2. Keep in mind that super user privileges are typically needed for shell commands involving virtual machines.

```
**Listing 29.2: Exploring the `virsh` shell**
$ `virsh`
Welcome to `virsh`, the virtualization interactive terminal.
Type: 'help' for help with commands
'quit' to quit
virsh # `exit`
$
```

You don’t have to enter the `virsh` shell in order to manage your virtual machines. The various `virsh` commands can be entered directly from the Bash shell, which makes it useful for those who wish to use the commands in shell scripts to automate virtual machine administration. An example of using the `virsh` utility interactively is shown in Listing 29.3.