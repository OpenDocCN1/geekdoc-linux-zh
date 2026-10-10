![](bbox=[0.21, 0.06, 0.81, 0.35])

Figure 10-2. The Unix Kernel Configuration tool

periods of time. (An example is support for floppyl disks; you'll rarely need this feature, but it's a good idea to have it nonetheless. Enabling that support, on the other hand, means the kernel requires more room in memory, which means less room for applications.)

With the module system, the kernel designers have created a way for parts of the kernel, called modules, to be dynamically loaded and unloaded from the kernel as needed. Features not often used can thus be enabled but won't waste memory when they aren't being used. Thankfully, the kernel can automatically determine what to load and when; you enjoy the benefits of streamlined running without the burden of having additional management tasks.

> **NOTE:** Traditionally, kernels have been written to require that all components, regardless of frequency of use, reside in memory at all times. Today's typical Linux kernels, however, only keep in memory the absolute core of the system, which is always needed. Device drivers and certain networking features are now supported as modules.