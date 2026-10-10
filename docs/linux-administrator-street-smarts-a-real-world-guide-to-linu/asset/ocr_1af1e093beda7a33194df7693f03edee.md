# ## Reviewing Existing Systems

If you have access to existing Linux computers that run software similar to what you plan for your new system, you can review their partitions. You can use `df` to do this job:

```
```
$ df
Filesystem      1K-blocks      Used Available Use% Mounted on
/dev/sdb6          977180     362768     614412  38% /
udev             256024       188      255836   1% /dev
/dev/sdb5         6291260    4820608    1470652  77% /usr
/dev/sda7         2564012    346868     2217144  14% /usr/local
/dev/sda8         3145628     832012    2313616  27% /usr/portage
/dev/sdb7         2097084    163748     1933336   8% /var
/dev/sdb12        17825244  11834228    5991016  67% /home
/dev/sda1         101089      3511       61803  37% /boot
```
```

This example shows seven partitions and one virtual filesystem (udev, mounted at /dev). Pay particular attention to the partitions' sizes (the `1K-blocks` column, which shows the file-system sizes in kilobytes) and to how full each partition is (the `Use%` column). The partition device names in the first column are unimportant for your purposes, but the mount points in the final column are important. Figure 5.1 shows the filesystems from this example (except for /dev, which isn't a disk filesystem) in graphical form, which should help you visualize how they're organized.

**FIGURE 5.1** Linux enables you to access partitions as directories in its directory tree.

![](bbox=[0.2, 0.57, 0.8, 0.98])