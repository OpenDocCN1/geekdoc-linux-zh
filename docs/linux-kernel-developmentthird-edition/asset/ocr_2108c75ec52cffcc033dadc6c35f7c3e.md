Linux distributions generate the mapping automatically and keep it up to date on each boot. To build the module dependency information, as root simply run

```
```
depmod
```
```

To perform a quick update, rebuilding only the information for modules newer than the dependency information, run as root

```
```
depmod -A
```
```

The module dependency information is stored in the file /lib/modules/version/modules.dep.

# Loading Modules

The simplest way to load a module is via insmod. This utility is basic. It simply asks the kernel to load the module you specify. The insmod program does not perform any dependency resolution or advanced error checking. Usage is trivial. As root, simply run this command:

```
```
insmod module.ko
```
```

Here, module.ko is the filename of the module that you want to load. To load the fishing pole module, you would run this command as root:

```
```
insmod fishing.ko
```
```

In a similar fashion, to remove a module, you use the rmmod utility. As root, simply run the following, where module is the name of an already-loaded module:

```
```
rmmod module
```
```

For example, this command removes the fishing pole module:

```
```
rmmod fishing
```
```

These utilities, however, are unintelligent. The utility modprobe provides dependency resolution, error checking and reporting, configurable behavior, and more advanced features. Its use is highly encouraged.

To insert a module into the kernel via modprobe, run as root:

```
```
modprobe module [ module_parameters ]
```
```

Here, module is the name of the module to load. Any following arguments are taken as parameters to pass to the module on load. See the section “Module Parameters” for a discussion on module parameters.

The modprobe command attempts to load not only the requested module, but also any modules on which it depends. Consequently, it is the preferred mechanism for loading kernel modules.

The modprobe command can also be used to remove modules from the kernel. To remove a module, as root, run

```
```
modprobe -r modules
```
```