# Installing a Kernel tar File

```
cd /usr/src
mkdir linux-version
rm linux
ln -s linux-version linux
zzvf linux-version.tar.gz
```

where version is the version of the Linux Kernel contained in the tar file. Once the file is installed, you can build the kernel by following the procedure given in the next chapter.

![](bbox=[0.137, 0.442, 0.213, 0.489])

Some kernel archives store kernels compressed using the BZIP utility, which yields smaller archive files. For instructions on using the BZIP utility, see its man page.

# Kernel Modules

Kernel modules are files that contain dynamically loadable kernel components, such as device drivers. Linux 2.0 required external assistance to load and unload modules; however, Linux 2.2 introduced the kmod thread that automatically loads modules when needed.

This section describes the location where kernel modules reside, the kernel module configuration file /etc/conf.modules, and the principal commands for managing kernel modules:

+   - depmod, which creates a database that describes module dependencies
- lsmod, which lists loaded modules
- modprobe, which loads kernel modules
- rmmod, which unloads kernel modules