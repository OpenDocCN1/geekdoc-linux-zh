# ## OPTIONS

*disk_image* is a raw hard disk image for IDE hard disk 0. So targets do not need a disk image.

Standard options:

+   - **-h**
+       - Display help and exit
+     - **-version**
+       - Display version information and exit
+     - **-machine [type=*na*\],prop=value[,...]]**
+       - Select the elated machine by *na*. Use `-machine help` to list available machines.
+       - Supported machine properties are:
+         - **accel=accels1[:accels2[...]]**
+           - This is used to enable an accelerator. Depending on the target architecture, kvm, xen, or tcg can be available. By default, tcg is used. If there is more than one accelerator specified, the next one is used if the previous one fails to initialize.
+         - **kernel_irqchip=on|off**
+           - Enables in-kernel irqchip support for the chosen accelerator when available.
+         - **vmport=on|off|auto**
+           - Enables elation of VMware 10 port, for vmmouse etc. auto says to select the value based on accel. For accel=xen the default is off otherwise the default is on.
+         - **kvm_shadow_m=size**
+           - Defines the size of the KVM shadow MMU.
+         - **dump-guest-core=on|off**
+           - Include guest mory in a core dump. The default is on.
+         - **m-rge=on|off**
+           - Enables or disables mory rge support. This feature, when supported by the host, de-duplicates identical mory pages among VMs instances (enabled by default).
+         - **iom=on|off**
+           - Enables or disables elated Intel IOMMU (VT-d) support. The default is off.
+         - **aes-key-wrap=on|off**
+           - Enables or disables AES key wrapping support on s390-ccw hosts. This feature controls whether AES wrapping keys will be created to allow execution of AES cryptographic functions. The default is on.
+         - **dea-key-wrap=on|off**
+           - Enables or disables DEA key wrapping support on s390-ccw hosts. This feature controls whether DEA wrapping keys will be created to allow execution of DEA cryptographic functions. The default is on.

- **-cpu** *model* Select cpu *model* (-cpu help for list and additional feature selection) **-smp [cpus=]*n*,cores=*cores*],threads=*threads*],sockets=*sockets*],maxcpus=*maxcpus*]] Silate an SMP system with *n* CPUs. On the pc target, up to 255 CPUs are supported. On Sparc32 target, Linux limits the nuer of usable CPUs to 4. For the pc target, the nuer of cores per