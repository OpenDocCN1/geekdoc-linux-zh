# # Make Dependencies

To be sure that everything that needs recompiling is compiled, you must build a list of dependencies for the source tree. Do this by typing

```
# make dep
```

# # Build the Kernel

To build the kernel, type

```
# make bzImage
```

You might want to redirect output to a file, like this:

```
# make bzImage >& make.log
```

> **Background Material**
> 
> You can try make zImage, but it is useful for small kernel images. If your kernel is too big, use make bzImage.

# # Build Modules

If you answered M to any questions, you need to build all kernel modules. To do this, type

```
# make modules
```

As before, you might want to redirect output to a file, like this

```
# make modules >& make.log.make_modules
```

# # Install Modules

To install modules, type

```
# make modules_install
```

This installs modules in /lib/modules/x.y.z, where x.y.z is the kernel version.

# # Install the Kernel

The compiled kernel will be in /usr/src/linux/arch/i386/boot/bzImage (or ...zImage if you used make zImage).

To install the kernel, copy this file to /boot. Do not overwrite your existing kernel (which is likely called /boot/vmlinuz-2.2.5-modular or something similar). Keep the