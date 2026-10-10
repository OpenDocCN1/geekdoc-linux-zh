workstation, you can install the modules directly to the target file system. The following example assumes the latter.

```
$ \text{make ARCH=arm CROSS\_COMPILER=pacable\_be-} \n\quad \text{INSTALL\_MOD\_PATH=}/home/chris/sandbox/coyote-target \n\quad \text{modules install}
```

This places all your modules in the directory coyote-target, which on this example system is exported via NFS and mounted as root on the target system.$^{3}$

# 8.1.6 Loading Your Module

Having completed all the steps necessary, we are now in a position to load and test the device driver module. Listing 8-5 shows the output resulting from loading and subsequently unloading the device driver on the embedded system.

# Listing 8-5

# Loading and Unloading a Module

```
$ \text{modprobe hello1} \quad \text{// Load the driver} \n\text{Hello Example Init} \n$ \text{modprobe -r hello1} \quad \text{// Unload the driver} \n\text{Hello Example Exit} \n$
```

You should be able to correlate the output with our device driver source code found in Listing 8-1. The module does no work other than printing messages to the kernel log system via printk(), which we see on our console.$^{4}$ When the module is loaded, the module-initialization function is called. We specify the initialization function that will be executed on module insertion using the module\_init() macro. We declared it as follows:

```
module\_init(hello\_init);
```

In our initialization function, we simply print the obligatory hello message and return. In a real device driver, this is where you would perform any initial resource allocation and hardware device initialization. In a similar fashion, when we unload the module (using the modprobe -r command), our module exit routine is called.