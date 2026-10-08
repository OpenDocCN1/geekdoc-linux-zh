# CHAPTER 10 | Kernel Security Mitigation

# Install Required Development Tools

If you haven't already installed the development tools described earlier in this chapter, do so now. As described earlier in this chapter, you will need development tools to compile and customize the kernel. The actual packages to be installed vary by distribution and release.

# Navigate to the Directory with the Source Code

The directory with the source code varies by distribution. Details described earlier in this chapter. That directory may have a name like /usr/src/linux-2.6.32/. On Red Hat systems, it may be named something like /usr/src/redhat/BUILD/kernel-2.6.18/linux-2.6.18.x86_64/. Once in that directory, you'll need a baseline configuration in the .config file in the local directory.

Standard architecture-specific configurations are available in configs/ subdirectory. Alternatively, you can copy the configuration of the currently loaded kernel from /boot/config-uname -r file, or you can process the current configuration with the make oldconfig command.

If you've compiled the kernel before, it's best to make sure any files that remain from previous custom kernels are clean with the following command:

```
# make clean
```

# Open a Kernel Configuration Tool

Now it's time to configure the kernel. Open a kernel configuration tool. For example, the make menuconfig command opens the console-based tool described earlier in this chapter. While other kernel configuration tools are available, they're functionally equivalent to this console-based tool.

When changes are made, you're prompted to save those changes. If those changes are successfully saved, you'll see it in the ls -l .config command, which should reflect the current date and time.

# Compile the Kernel with the New Custom Configuration

Before compiling the kernel, open the file named Makefile in the local directory. Look at the EXTRAVERSION directive. It adds the suffix to be added to the newly compiled kernel. You may want to add an identifier to that directive; I've added my name here:

```
EXTRAVERSION = -prep.mike
```

Be aware, it takes time to compile a kernel. On slower systems, the process may even take a couple of hours. Make sure there's at a couple of gigabytes of free space on the volume where the kernel is being compiled. If the volume fills up before the process is complete, you'll have to delete unused files and start again.

![](bbox=[0.935, 0.715, 0.996, 0.996])