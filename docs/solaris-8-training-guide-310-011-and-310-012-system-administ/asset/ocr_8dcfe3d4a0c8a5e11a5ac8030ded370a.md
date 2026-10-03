at runtime. After these modules are no longer in use, they can be unloaded. Modules are kept in memory until that memory is needed. The modinfo command provides information about the modules currently loaded on a system.

When the kernel is loading, it reads the /etc/system file where system configuration information is stored. This file modifies the kernel's parameters and treatment of loadable modules. It specifically controls the following:

+   - The search path for default modules to be loaded at boot time, as well as the modules not to be loaded at boot time
- The modules to be forcibly loaded at boot time rather than at first access
- The root type and device
- The new values to override the default kernel parameter values

The following is an example of the default /etc/system file:

```
*ident      "@(#)system      1.18    97/06/27 SMI" /* SVR4 1.5 */
*
* SYSTEM SPECIFICATION FILE
*
* moddir:
*
*Set the search path for modules. This has a format similar to the
*csh path variable. If the module isn't found in the first directory
*it tries the second and so on. The default is /kernel /usr/kernel
*
*Example:
*moddir: /kernel /usr/kernel /other/modules
* root device and root filesystem configuration:
*
*The following may be used to override the defaults provided by
*the boot program:
*
*rootfs:          Set the filesystem type of the root.
*
*rootdev:         Set the root device. This should be a fully
                  expanded physical pathname. The default is the
                  physical pathname of the device where the boot
                  program resides. The physical pathname is
                  highly platform and configuration dependent.
```