By creating a symbolic link to /usr/src/linux-2.6, it is possible to allow multiple kernel versions to be compiled and tailored for different functions: You just change the symbolic link to the kernel directory on which you want to work.

> **CAUTION**
> 
> The correct symbolic link is critical to the operation of make. Always have the symbolic link point to the version of the kernel sources with which you are working.

# # Patching the Kernel

It is possible to patch a kernel to the newest Linux kernel version, as opposed to downloading the entire source code. This choice can be beneficial for those who are not using a high-speed broadband connection. (A typical compressed kernel source file is nearly 30MB for a download time of about 10 minutes on a 512Kb DSL connection; adjust accordingly for your connection.) Whether you are patching existing sources or downloading the full source, the end results are identical.

Patching the kernel is not a mindless task. It requires the user to retrieve all patches from her current version to the version to which she wants to upgrade. For example, if you are currently running 2.6.1 (and have those sources) and want to upgrade to 2.6.8, you must retrieve the 2.6.2, and 2.6.3 patch sets, and so on. After they are downloaded, these patches must be applied in succession to upgrade to 2.6.8. This is more tedious than downloading the entire source, but useful for those who keep up with kernel hacking and want to perform incremental upgrades to keep their Linux kernel as up-to-date as possible.

To patch up to several versions in a single operation, you can use the `patch-kernel` script located in the kernel source directory for the kernel version you currently use. This script applies all necessary version patches to bring your kernel up to the latest version.

The format for using the `patch-kernel` script looks like this:

```
patch-kernel source_dir patch_dir stopversion
```

The source directory defaults to /usr/src/linux if none is given, and the `patch_dir` defaults to the current working directory if none is not supplied.

For example, assume that you have a 2.6.6 kernel code tree that needs to be patched to the 2.6.8 version. The 2.6.7 and 2.6.8 patch files have been downloaded from ftp.kernel.org and are placed in the /patch directory in the source tree. You issue the following command in the /usr/src/kernels/linux-2.6 directory:

```
# scripts/patch-kernel /usr/src/kernels/linux-2.6.15
>/usr/src/kernels/linux-2.6.15/patch
```

Each successive patch file is applied, eventually creating a 2.6.8 code tree. If any errors occur during this operation, files named xxxi or xxxrej are created, where xxx is the