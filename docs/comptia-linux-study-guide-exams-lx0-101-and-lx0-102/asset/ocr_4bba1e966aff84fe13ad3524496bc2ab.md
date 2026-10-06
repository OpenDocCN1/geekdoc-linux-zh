This output has been edited for brevity. Although outputs this short
possible with certain configurations, they're rare.

The most important column in this output is the first one, labeled Module; this column
sifies the names of all the modules that are currently loaded. You can learn more about
these modules with modinfo, as described shortly, sometimes their purpose is fairly
obvious. For instance, the cdrom module provides access to the optical drive.

The column used by insmod output describes what its using the module. All the
entries have a number, which indicates the number of other modules or processes that are
using the module. For instance, in the preceding example, the isofs module (used to access
CD-ROM files) isn't in use, as revealed by its 0 value; but the vfat module
(to read VFAT disk partitions and files) is being used, as shown by the value of
1. If one of the modules is used by another module, the module's name appears
to the Used by column. For instance, the isofs module relies on the 21b_inflate module,
so the latter module's column includes the isofs module. This information
can be useful when you're managing modules. For instance, if your system produced
t preceding output, you couldn't directly remove the 21b_inflate module because it's being
used by the isofs module; but you could remove the isofs module, and after doing so, you
would remove the 21b_inflate module. (Both modules would need to be added back to
read most cmdmod, though.)

The insmod command displays information only about kernel modules,
not about drivers that are compiled directly into the Linux kernel. For this
reason, a module may need to be loaded on one system but not on another
to use the same hardware because the second system may compile the
relevant driver directly into the kernel.

# Loading Kernel Modules

Linux enables you to load kernel modules with two programs: insmod and modprobe. The
insmod program inserts a single module into the kernel. This process requires you to have
already loaded any modules on which the module're loading relies. The modprobe pro-
gram, by contrast, automatically loads any depended-on modules and so is generally the
preferred way to do the job.

In practice, you may not need to use insmod or modprobe to load modulesecause Linux can load them automatically. This ability relies on the ker-
el's module auto-loader, which must be compiled into the kernel,
and on various configuration files, which are also required for modprobe and
s other tools. Using insmod and modprobe can be useful for testing new
modules or for working around problems with the auto-loader, though.