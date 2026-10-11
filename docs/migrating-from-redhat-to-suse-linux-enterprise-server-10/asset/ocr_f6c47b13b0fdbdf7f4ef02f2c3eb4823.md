The command shutdown can also be supplied with a warning message, such as the following:

```
shutdown +5 "The new hard drive has arrived"
```

If a shutdown planned for a later time should not be carried out after all, you can revoke the shutdown by entering **shutdown -c**.

# ### Compare Start Scripts between RHEL and SLES 10

The following table lists the files and directories with comparable functionality:

# **Table 5-3**

| **RHEL 4** | **SLES 10** |
| :--- | :--- |
| /etc/rc.d/init.d/ | /etc/init.d/ |
| /etc/rc.d/rcX.d/ | /etc/init.d/rcX.d/ |
| /etc/rc.d/init.d/service | /etc/init.d/service |
| /etc/rc.d/rc.sysinit | /etc/init.d/boot |
| /etc/rc.d/rc | /etc/init.d/rc |

In SUSE Linux Enterprise Server 10, there is a symbolic link from /etc/rc.d/ pointing to /etc/init.d/, as there is one on RHEL pointing from /etc/init.d/ to /etc/rc.d/. Therefore, administrators familiar with one system will easily find the files they are looking for in the other system.