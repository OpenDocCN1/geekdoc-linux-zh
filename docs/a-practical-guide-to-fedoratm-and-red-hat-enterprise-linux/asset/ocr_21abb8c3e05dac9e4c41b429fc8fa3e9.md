After you have installed a system, you might want to reconfigure and build a new Linux kernel. Fedora/RHEL comes with a prebuilt kernel that simplifies the installation process. However, this kernel might not be properly configured for all system features. By configuring and building a new kernel, you can create one that is customized for a system and its unique needs. A customized kernel is typically smaller than a generic one. However, compiling and maintaining a custom kernel takes a lot of time and work.

Sometimes you do not need to build a new kernel. Instead, you can dynamically change many aspects of the installed kernel. Two ways to make these changes are by using boot command-line parameters (page 70) or by modifying /etc/sysctl.conf, which **sysctl** (next) reads when the system boots.

You can add the same parameters you use on the boot command line to /boot/grub2/grub.cfg or to its symbolic link, /etc/grub2.cfg. For example, **acpi=off** prevents **acpid** (the advanced configuration and power interface daemon) from starting. See page 70 for more information.

**sysctl**  
The **sysctl** utility can modify kernel parameters while the system is running. This utility takes advantage of the facilities of /proc/sys, which defines the parameters that **sysctl** can modify.

The command **sysctl -a** displays a complete list of **sysctl** parameters. An example of displaying and changing the **domainname** kernel parameter follows. The double quotation marks are not required in this example, but you must quote any characters that would otherwise be interpreted by the shell. You must work with **root** privileges when you change a parameter.

```
```bash
$ sysctl kernel.domainname
kernel.domainname = (none)
$ su -c 'sysctl -w kernel.domainname="example.com"'
kernel.domainname = example.com
$ sysctl kernel.domainname
kernel.domainname = example.com
```
```

# Have the installation medium handy when you build a new kernel

**caution**  
When you have one Linux kernel to install a new version or to change the configuration of the existing version, make sure you have the installation medium handy. This disk allows you to reboot the system, even when you have destroyed the system software completely. Having this medium available can mean the difference between momentary panic and a full-scale nervous breakdown. Refer to “Rescue an Installed System” on page 456 for more information.

# Secure Boot

**tip**  
On newer machines, Secure Boot might keep a custom kernel from booting. On these machines you need to disable Secure Boot or set up your own keys and sign the kernel with them. For more information visit both **fedoraproject.org/wiki/Secureboot#Questions_and_Answers** and **jwboyer.livejournal.com/46149.html**.