```
oracleasm-2.4.9-e-smp-1.0.0-1.i686.rpm
oracleasm-2.4.9-e-summit-1.0.0-1.i686.rpm
oracleasmlib-1.0.0-1.i386.rpm
oracleasm-support-1.0.0-1.i386.rpm
```

The list can be broken down into three parts.

+   
+   * The driver component that is used with the appropriate Linux kernel. Notice that the first four items in the list have the Linux kernel revision in the name of the file. These files support the Linux 2.4.9 kernel standard edition, enterprise, smp, and IBM summit kernels.
+   * The ASM library shared object file.
+   * The Oracle ASM support files. These are the programs used to configure and maintain the ASM volumes.
+   

In order to install the proper files, select the driver component(s) suitable for your system, the Oracle ASM library module, and the support files using rpm, as shown next:

```
oracleasm -rpm -Uvh oracleasm-2.4.9-e-1.0.0-1.i686.rpm oracleasmlib-1.0.0-1.i386.rpm oracleasm-support-1.0.0-1.i386.rpm
```

This will install all of the files you need to begin working with ASM. Next, the disk groups must be configured with ASM.

**Configuring ASM Drives** There are two steps necessary to set up and configure ASM. First, ASM must be configured. This configuration is accomplished by running the command /etc/init.d/oracleasm configure, as shown next. The second step is to configure partitions to use ASM.

# # Configuring the ASM Library Driver

The ASM configuration script sets up the necessary configuration files and services in order to run ASM. The following specific tasks are done by running oracleasm configure:

+   
+   * The /etc/sysconfig/oracleasm file is created. This file is used when the Oracle ASM service starts up.
+   * The /dev/oracleasm directory is created with the disks and subdirectories.
+   * The oracleasm kernel module is loaded. You can see this by running lsmod.
+   * The ASM library driver filesystem is mounted. You can see from the mount command that oracleasmfs is mounted on /dev/oracleasm.
+