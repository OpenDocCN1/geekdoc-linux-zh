**3. Extract the source code to the TCFS kernel module into the Linux source tree (the Linux source tree on Red Hat systems is in /usr/src/linux).**

```
# cd /usr/src
# tar xzvf /usr/src/custom/tcfs/tcfs-2.2.2/tcfs-2.2.2.tar.gz
```

**4. Extract the TCFS library into the working directory.**

```
# cd /usr/src/custom/tcfs/tcfs-2.2.2
# tar xzvf tcfslib-0.3.1.tar.gz
```

This will create the subdirectory /usr/src/custom/tcfs/tcfs-2.2.2/tcfslib-0.3.1. Next you will need to compile and install the libraries and the TCFS PAM module. Execute

```
# cd tcfslib-0.3.1
# make
# make install
# make pam_module
# cp pam_tcfs.so /lib/security
```

to complete this task. Note that the output from these commands has been omitted, as will be the case throughout these steps.

**5. You will need to install the user and key management tools. Extract and make as shown below.**

```
# cd /usr/src/custom/tcfs/tcfs-2.2.2
# tar xzvf tcfsutils-1.2.1.tar.gz
```

Change the Makefile in /usr/src/custom/tcfs/tcfs-2.2.2/tcfsutils-1.2.1/src so that the lines appear as follows (yes, is instead of if in the comments).

```
# Uncomment line below is you use GLIBC
LOADLIBES=-lncrypt -ltcfs
# Uncomment the line below is you do not have GLIBC
LOADLIBES=-ltcfs
```

Then

```
# cd /usr/src/custom/tcfs/tcfs-2.2.2/tcfsutils-1.2.1/src
# make
# make install
```

# **WARNING!**

> The next three steps involve replacing system utilities. Before proceeding you need to make sure that doing so will not disturb other applications or system utilities on your computer. To do this, verify that the version numbers of the utilities in these next three steps are greater than or equal to those utilities currently installed on your system. To be on the safe side, you may wish to make copies of the programs that will be installed (see Table 15.5 on page 418) prior to proceeding.