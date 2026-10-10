between vPars and the monitor.

An Ignite-UX server is used as the source depot for the **vparboot** installation process. If an Ignite-UX server does not already exist for use with this process, install and configure one, preferably on another system, starting with steps 1 through 3 below. If an Ignite-UX server does exist, or is older than revision B.3.4.115, it will need to be updated. If your Ignite-UX server is already at revision B.3.4.115, continue with step 4 below.

# **1) Obtain Ignite-UX software.**

Sources include CDROM, *software.hp.com*, and SD-UX depot files.

Note: the revision of Ignite-UX supported for the first release of vPars is **B.3.4.115:**

```
```
= what /opt/ignite/bin/ignite
/opt/ignite/bin/ignite:
ignite user interface $Revision: 10.643 $
Ignite-UX Revision B.3.4.115
install/h $Revision: 10.102 $
```
```

This revision can be found on the September 2001 application distribution. Although previous versions of Ignite-UX may work, they are not supported for use with vPars, and may have problems with the relocatable **WINSTALL** file, which was built using libraries based on the B.3.4.115 revision of Ignite-UX.

# **2) Install or update Ignite-UX software.**

Use *swinstall* to install Ignite-UX.

# **3) Update *PATH*.**

Add the following search path to your login script(s):

```
```bash
export PATH=${PATH}:/opt/ignite/bin
```
```