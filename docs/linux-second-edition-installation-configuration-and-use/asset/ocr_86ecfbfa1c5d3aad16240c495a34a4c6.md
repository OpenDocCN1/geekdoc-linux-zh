# 126 LINUX FUNDAMENTALS

![](bbox=[0.265, 0.055, 0.945, 0.375])

**Figure 5.1** The process hierarchy.

Unfortunately, the number of distributions differs between SuSE and Debian slightly different distributions. The meaning of each is documented in /etc/initab.

At system-start, the default runlevel is determined by the initdefault line in /etc/initab. root can also change the runlevel during operation using it (x must be substituted by a number or letter that specifies the runlevel). For example, for some maintenance tasks it makes sense to change to include single user mode. The runlevel is also changed by shutdown and `Ctrl+Alt+Del` – Linux to runlevel 6 for shutting down.