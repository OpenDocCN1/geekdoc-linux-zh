# Packages Required to run NS 2

NS 2 requires the following packages to run:

+   - Tcl release 8.3.2
+   - Tk release 8.3.2
+   - OTcl release 1

# Installing NS2 on Linux System

# Step#1: Download and Install NS2

The process of installing NS2 is simple. The most recent version of NS 2 is 2.34. The “all-in-one” package provides all the packages required to run NS2. You can download the all-in-one package from the NS2 home page into /usr/src directory and extract it as follows:

```
```
[root@netmon opt]# cd     /usr/src/
[root@netmon src]# tar -xzvf ns-allinone-2.34.tar.gz
[root@netmon src]# cd ns-allinone-2.34
```
```

In the same directory, there is a script named “install” that can be used to configure, compile and install the required and optional NS 2 components. There is no interaction with the user while installing NS 2 components: the script is completely automated. You must execute the script as root user or administrator so that the installation of binaries is completed:

```
```
[root@netmon ns-allinone-2.34]# ./install
```
```

When the installation process is complete, the following message appears on your shell:

```
```
Nam has been installed successfully.
Ns-allinone package has been installed successfully.
Here are the installation places:
tcl8.4.11:      /usr/src/ns-allinone-2.34/bin, include, lib}
tk8.4.11:       /usr/src/ns-allinone-2.34/bin, include, lib}
otcl:           /usr/src/ns-allinone-2.34/otcl-1.11
tclc:           /usr/src/ns-allinone-2.34/tc1-1.17
ns:             /usr/src/ns-allinone-2.34/ns


nam:    /usr/src/ns-allinone-2.34/nam-1.11/nam
xgraph:/usr/src/ns-allinone-2.34/xgraph-12.1
gt-itm:  /usr/src/ns-allinone-2.34/itm, edriver, sgb2alt, sgb2ns, sgb2comms, sgb2hierms

Please     put    /usr/src/ns-allinone-2.34/bin; /usr/src/ns-allinone-2.34/tcl8.4.11/unix;/usr/src/ns-allinone-2.34/tk8.4.11/unix  into your  PATH environment; so that you'll be able to run itm/tclsh/wish/xgraph.

IMPORTANT  NOTICES:

(1).  You  MUST  put  /usr/src/ns-allinone-2.34/otcl-1.11,  /usr/src/ns-allinone-2.34/tlb,
into your LD_LIBRARY_PATH environment variable.
If it complains about x libraries, add path to your x libraries into LD_LIBRARY_PATH.
If you are using csh, you can set it like:
setenv LD_LIBRARY_PATH  <paths>
If you are using sh, you can set it like:
```
```