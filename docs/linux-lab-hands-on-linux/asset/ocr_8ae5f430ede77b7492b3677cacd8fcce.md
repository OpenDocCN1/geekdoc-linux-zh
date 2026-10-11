To change the kernel operating parameters that are not configurable at boot time.

# ## Kernel Modules

+   - Modular kernel Components
+   	- Components not needed at boot
+   	- Peripheral device drivers
+   	- Supplementary file systems
+   	- Modules Configurable at load time
+   - /lib/modules
+   - Controlling Modules: lsmod , insmod, rmmod
+   - Controlling modules intelligently: modprobe, depmod

# ### Modular Kernel Components

Many components of the kernel can be compiled as dynamically modules. This increases kernel functionality without increasing the size of the kernel loaded at boot time. Good candidates for modularization are any supplementary capabilities that are not needed at boot time, including peripheral device drivers and supplementary file systems.

# ### The /lib/modules directory

Kernel modules reside in *//lib/modules/(kernel-version)*, which in turn contains various subdirectories according to the module type, such as *block*, *cdrom*, *net*, and *scsi*. The directory name must match the kernel version. Type the following commands in the command line to display the release number:

```
```
# uname -r or uname -a
```
```

# ### Controlling Modules

Modules are generally loaded on demand by the kernel. *lsmod* lists the modules currently resident in the kernel. The kernel can be prompted to load a particular module with *insmod*, and various module parameters can be specified as command line arguments. *rmmod* module is used to unload a module if it is idle.

To list the modules, run the following command

```
```
[root@netmon opt] # lsmod
```
```

To load a particular module

```
```
[root@netmon opt] # insmod e100-k0
```
```

To unload module

```
```
[root@netmon opt] # rmmod e100
```
```