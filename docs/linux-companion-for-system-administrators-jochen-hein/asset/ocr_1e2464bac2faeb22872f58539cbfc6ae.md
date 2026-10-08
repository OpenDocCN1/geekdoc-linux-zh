# 80 CONFIGURATION AND ADMINISTRATION

# 4.1.3 Updating the kernel

A kernel update can be carried out in two ways. You can install a completely new kernel, or the changes in the source code can be transferred to the kernel sources by means of the patch program (see also Chapter 10).

# Complete installation of the kernel

Installing a new kernel is quite easy. First, the old kernel sources should be saved, so that the old kernel can be used again in case an error occurs. If you have enough hard disk space, it is sufficient to rename the complete path. Otherwise, it would be sensible to execute make clean and then store the kernel in a (compressed) archive (for example, by using tar). Subsequently, the new kernel sources can be unpacked and the already known process of kernel configuration and compilation can be run. Many system-related programs depend on the fact that at least the make step is performed. The necessary commands are shown in Listing 4.3.

```
(Linux):/usr/src/linux# make clean
(Linux):/usr/src/linux# cd .
(Linux):/usr/src/linux# mv linux linux.old
(Linux):/usr/src/linux# tar xvzf /tmp/linux-1.2.2.tar.gz
(Linux):/usr/src/linux# cd linux
(Linux):/usr/src/linux# make config
```

Listing 4.3 Complete kernel update.

# Patching the kernel

The second method of updating the kernel is known as patching the kernel. Since the source code of two kernel versions is often nearly the same, much less data has to be transferred for an update. A patch only contains the changes from one version to the next. Thus, if you want to use a kernel that is several versions more recent, it is even easier to obtain the new sources than to execute all patches in the correct order.

If these aspects are taken into consideration, updating the kernel is quite simple. As an example, we show the update from kernel version 1.2.1 to version 1.2.2. The advantage of patching is that you find all changes to the source text in a relatively well-structured way. If you have some programming experience, you should definitely have a good look at the patches before you install them. The zmore program used in the present example is not contained in the widely used