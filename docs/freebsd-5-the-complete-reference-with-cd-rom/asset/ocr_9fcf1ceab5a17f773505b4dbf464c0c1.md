# ## Preparing to Run Linux Programs

FreeBSD isn't configured to run Linux programs in a basic installation. To do this, perform these steps:

+   1.  **Install the Linux base port.** The *linux\_base* package includes the core Linux libraries and support tools. Most of these reside in the `/compat/linux` directory tree. You can install this package as you do other packages, as described in Chapter 11.
+   2.  **Configure hostname resolution.** Some Linux programs have problems resolving hostnames into IP addresses when run with the default configuration. If you have this problem, you should edit the `/compat/linux/etc/host.conf` file so that it contains the following lines:
+   
+       ```
+       order hosts,bind
+       multi on
+       ```
+   3.  **Start the Linux compatibility mode.** Type `1 linux` to start the Linux compatibility mode. Thereafter you should be able to run Linux programs. If you want your system to enable this mode automatically after you boot, add the following line to your `/etc/rc.conf` file, if it's not already present:
+   
+       ```
+       linux_enable="YES"
+       ```
+   
+       At this point, FreeBSD should support Linux binaries. To check that it does, you can use the `kldstat` program, which returns information on kernel modules loaded on your system, including FreeBSD's Linux compatibility module. A properly working Linux support layer should produce output that resembles the following:

```
```
$ kldstat
Id Refs Address     Size      Name
1   5   0xc0100000  3ef2dc    kernel
2   1   0xc1cb2000  16000     linux.ko
```
```

There may be more lines displaying additional modules. The key is that a line referencing the *linux.ko* kernel module should be present, such as the line with an ID of 2 in the preceding example.

# ## Reconfiguring and Running Linux Programs

FreeBSD and Linux use the same basic format for their program files. This format is known as the *Executable and Linking Format* (ELF). Although the basic format is the same, a few details differ, and these sometimes cause FreeBSD to not recognize Linux binaries as valid. If FreeBSD reports that a Linux binary isn't valid, you must use the