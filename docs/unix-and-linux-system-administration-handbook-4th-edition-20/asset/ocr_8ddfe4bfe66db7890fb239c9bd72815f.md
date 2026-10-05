# Loadable kernel modules in Linux

Although loadable drivers are convenient, they are not 100% safe. Any time you load or unload a module, you risk causing a kernel panic. Don't try out an untested module when you are not willing to crash the machine.

Like other aspects of device and driver management, the implementation of loadable modules is OS dependent. The sections below outline the commands and caveats appropriate for Solaris and Linux, which support more devices and allow administrator configuration than we do other examples systems.

# Loadable kernel modules in Linux

Linux is both more and less sophisticated than Solaris in its handling of loadable kernel modules, at least from the system administrator's point of view. Under Linux, almost anything can be built as a loadable kernel module. The exceptions are the root filesystem type, the device on which the root filesystem resides, and the PS/2 mouse driver.

Loadable kernel modules are conventionally stored under `/lib/modules/version`, where version is the version of your Linux kernel as returned by `uname -r`. You can inspect the currently loaded modules with the `lsmod` command:

```
`sudo /sbin/lsmod`
```

| Module | Size | Used by |
|---|---|---|
| ipmi_devintf | 13064 | 2 |
| ipmi_si | 36648 | 1 |
| ipmi_mshandler | 31488 | 2 ipmi_devintf,ipmi_si |
| iptables_filter | 6721 | 0 |
| ip_tables | 21441 | 1 iptables |

Loaded on this machine are the Intelligent Platform Management Interface modules and the `iptables firewall.

As an example of manually loading a kernel module, here is how we would insert the snarf module we set up in the following section:

```
`sudo insmod /path/to/snarf.ko`
```

We can also pass parameters to loadable kernel modules; for example,

```
`sudo insmod /path/to/snarf.ko io=0XXX irq=X`
```

Once a loadable kernel module has been inserted into the kernel, it can only be removed if you explicitly request its removal or if the system is rebooted. We could use `rmmod snarf` to remove our snarf module.

You can use `rmmod` at any time, but it works only if the number of current references to the module (listed in the `Used` column of `lsmod`s output) is 0.

You can also load Linux LKMs semiautom with `modprobe`, a wrapper for `insmod` that understands dependencies, options, and installation and removal procedures. `modprobe` uses the `/etc/modprobe.conf` file to figure how to handle each individual module.