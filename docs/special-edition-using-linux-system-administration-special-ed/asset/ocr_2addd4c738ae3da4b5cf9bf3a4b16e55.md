The + symbol indicates the line should be added to the `config.in` file and the - indicates that the line should be deleted from `config.in`. Edit the `config.in` file accordingly and reapply the remainder of the `config.in.rej` file with the following command:

```
# patch -p0 > config.in.rej
```

If there are no errors reported, you can delete the `config.in.rej` file. It is not deleted automatically by patch. Next you can proceed with the configuration and compilation steps, as we have discussed in the “Configuring the Kernel” and “Compiling the Kernel” sections earlier in the chapter.

Installing patches out of order or applying non-standard patches is another reason for errors. If you continue to get more errors, it is better to start from scratch with a clean source tree that you have not modified in any way. For example, unpack the original `linux-2.2.12.tar.gz` that you used to build your current version. Run `make mrproper` to clean up the source tree and then apply `patch-2.2.2.13`.

# ## Cleaning Up After Patching

After patching source trees a few times, you will notice file names with `.orig` extensions starting to accumulate. You can remove these out by running a find command as follows:

```
# cd /usr/src/linux
# find . -name '*.orig' -exec rm -f {} \;
```

An earlier version of patch created tilde files instead of `.orig` files. To remove these you can run the following find command instead:

```
# find . -name '*~' -exec rm -f {} \;
```

# ## Understanding Modules

Since Linux 2.0.x, modules have been introduced. These change the way kernels are built. In the past, any device driver or file system type that you needed access to had to be compiled into the kernel. For certain system configurations where the kernel had to occasionally support a lot of different devices, the kernel size would get very big, demanding a lot of system resources and resulting in performance degradation. To remedy this situation, modularized kernels were designed. This allows for building modules for infrequently used drivers or file systems. These modules can be loaded on demand, and later unloaded when they are no longer needed.

Good candidates for modules are a variety of Ethernet drivers, CD-ROM drivers, certain file system support drivers, and miscellaneous other modules.

Some changes in how modules are supported by the kernel have been made. In earlier kernels, a kernel daemon would load and unload modules on demand. In current modules, `kerneld` has been replaced by `kmod`. `kmod` also loads and unloads modules on demand but does not require an external program to be running; it runs as a thread within the kernel. When the