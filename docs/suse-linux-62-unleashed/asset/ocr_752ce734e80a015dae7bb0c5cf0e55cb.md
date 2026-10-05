# SuSE System Administration
PART III

While it is far more mnemonic to create a boot floppy using the command make zdisk, this is equivalent to using the dd command to copy the file directly to the disk device (that is, to the raw sectors of the disk):

dd if=/i386/zImage=/dev/fd0

# Tip

When you're creating a kernel for some other machine (such as a laptop), you can put the compressed kernel file and all modules into an alternate directory tree by adding the alternate values for the INSTALL PATH variable to make the command line:

```
INSTALL_PATH=/psitta \
INSTALL_MOD_PATH=/psitta ROOT_DEV=/dev/hda1 \
make bzlilo modules_install
```

This command will move the generated kernel, map, and module files to /psitta/mlinuz, /psitta/System.map, and /psitta/lib/modules, where you conveniently entirely the whole directory for shipment to the remote machine with the following:

```
cd /psitta && \
tar cf - vmlinuz System.map lib/modules/2.2.7 \
tar xCF / -
```

The make command will also run LILO, but because the /etc/lilo.conf file does not reference these /psitta files, there is no side effect.

The only potential side effect of this process is a possible change to files in /usr/include/linux, which may affect programs subsequently compiled on the build host. Some care be taken to ensure that the alternate kernel build does not leave unwanted changes in this directory on the build machine. Also, if the remote machine will be used to build software, you should copy the /usr/include/linux directory onto the remote machine after compiling the new kernel.

# Troubleshooting the New Kernel

/proc is your friend. With the 2.0 kernels, the pseudo-files in the /proc directory hold a wealth of diagnostic information and a simple means to set runtime parameters.

# System Information Files

The most frequently useful /proc diagnostic files are as follows: