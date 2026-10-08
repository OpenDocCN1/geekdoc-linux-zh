You may also want to enable **dhcp** if your network uses that to set up a network connection. For example the kernel setting would look like this:

```
kernel = "/boot/vmlinuz-2.6.20-1.3104-F7"
```

You use the **xm** command with the **create** option, followed by the configuration file. In this example there is a configuration file in /etc/xen called **my-newwvm1**, which is the same name as the virtual machine. Check the Man page for **xm domain.cfg** for detailed configuration options and examples.

```
xm create my-newwvm1
```

You can then connect to it with the **console** option.

```
xm console my-newwvm1
```

You can combine the two **xm** **commands** using the **-c** option for the console connection.

```
xm create -c my-newwvm1
```

You will still have to install the operating system you want to use. You can do this on a designated partition or logical volume, or use **virt-install**. You can install with a text-based system or use VNC for a virtual install.

# ### Managing Xen Virtual Machines with virt

After you have installed the system, you can then create a connection to it with **xm** command. To access a particular domain, use the **console** option and the domain name.

```
xm console my-newwvm1
```

If the domain no longer exists, you have to also create it and then connect.

```
xm create -c my-newwvm1
```

Check the **xm** options on the **xm** Man page for other operations you can perform on your virtual machines.

To access domains, you use the **xm** command. The **list** option lists your domains. The listing will include detailed information such as its domain ID, the CPU time used, memory used, and the domain state. The following lists your domains:

```
xm list
```

The **xm save** and **restore** options can be used to suspend and restart a domain.

Block devices such as partitions and CD-ROMs can be exported from the main domain to virtual domains. This allows a given virtual domain to use a particular partition. You can even share block devices between domains, though such shared devices should be read only.

To start and stop your domains, you can use the **xendomains** service script. The **xendomains** script will use **xm** with the **create** option to create a domain configured in the /etc/xen/auto directory. Place Xen domain configuration files in this directory for