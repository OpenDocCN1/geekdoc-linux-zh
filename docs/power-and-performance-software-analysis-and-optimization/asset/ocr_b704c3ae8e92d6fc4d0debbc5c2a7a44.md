# 7.1 Installation and configuration 121

```
$ ls -alh /proc/vtsspp
total 0
dr-xr-xr-x. 2 root vtune 0 Sep 12 23:08 ./
dr-xr-xr-x. 21 root ubuntu 0 Sep 12 23:56 ../
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .control
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .cpu_mask
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .debug
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .def_sav
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .targets
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .time_limit
-rw-rw-r-- 1 root vtune 0 Sep 12 23:17 .time_source
```

In earlier versions of VTune, there was a fourth driver, apwr,ko, which was part of the powerdk, as opposed to the sepdk, which the other three drivers belong. This driver was used for measuring some metrics, but was recently removed due to lack of usage. If the reader depends on this driver, the author recommends contacting Intel support.

# 7.1.1 BUILDING THE KERNEL MODULE

In order to build the sepdk drivers manually, there is a script entitled build-driver at ${VTUNE_INSTALL}/sepdk/src. Before running this script, ensure that the proper development tools, including GCC, GNU make, and the kernel development package, are installed. Additionally check the VTune release notes to determine whether the kernel version is supported. Typically VTune tracks the latest distros, such as Fedora, Ubuntu, and RHEL.

Running the build-driver script will build all three drivers, although there are also build-driver scripts within the vtsspp and pax subdirectories. These scripts are all interactive, prompting the user for which compiler to use, path to the kernel source and where to install them. The script can also run nonactively with the --interactive command-line argument. In interactive mode, the defaults for each option will be used, unless a different value is specified via command-line arguments. A full list of these arguments, such as c-compiler, --kernel-src-dir, and --install-dir, can be obtained by running build-driver --help. In case where the build fails on a newer kernel, contact Intel support.

Once the drivers are successfully built, they can be manually inserted into the kernel, or the init system can be configured to automatically insert them at boot. In the same directory as the build-driver script, there is also a script named boot-script. This script will automatically generate a sysv-style init script and then add it to the default runtime for the system.

Since the drivers are modules, it is simple to test if the boot script works. Simply reboot and check whether the modules were automatically loaded. This can be