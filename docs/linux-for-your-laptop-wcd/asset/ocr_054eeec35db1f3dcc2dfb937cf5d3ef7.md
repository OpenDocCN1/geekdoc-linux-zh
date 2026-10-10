The *PCMCIA* *drivers* need to be compiled to match the kernel they will be used with, or some or all of the modules may fail to load.
If you are not sure what to do, please consult the *PCMCIA-HOWTO*.

How would you like to set kernel-specific options?

+   1.  Read from the currently running kernel
+   2.  Read from the Linux source tree
+   Enter option (1-2) [2]:

Although the default option is to use the installation Linux source code, this code (especially with *Mandrake Linux*) might not match the kernel you're running on your notebook! A much safer approach is to choose 1 to use the currently running kernel driver options. After you press *Enter*, you'll see the following:

```
```
Kernel configuration options:

	Static in-kernel PCMCIA support is disabled.
	Symmetric multiprocessing support is disabled.
	PCI BIOS support is enabled.
	Advanced Power Management (APM) support is enabled.
	SCSI support is enabled.
	Networking support is enabled.
	Radio network interface support is enabled.
	Token Ring device support is enabled.
	Pasta switching is disabled.
	Module version checking is enabled.
	/proc filesystem support is enabled.
	Maximum physical memory: 1GB
```
```

System V init script layout (y/n) [y]:
You'll get a short report on your Linux kernel. (You might be surprised to see the kind of installed support you have!) Then you will be asked if your system uses a *System V* init script layout. Press *Enter* (or *y*) if you're using *Red Hat* or *Mandrake Linux*.
Top-level directory for RC scripts [ /etc/rc.d ]:

*Both Red Hat and Mandrake Linux use init scripts under the /etc/rc.d directory, so you can just press Enter.*

```
```
X Windows include files found.
/usr/X11R6/lib/libforms.so and /usr/X11R6/include/forms.h found.
Configuration successful.
```
```