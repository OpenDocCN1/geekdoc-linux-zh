# FIGURE 6-5 The Logical Volume Management tool

![](bbox=[0.11, 0.18, 0.92, 0.66])

If needed, you can install the system-config-lvm package with the following command:

```
# yum install system-config-lvm
```

If possible, test the options in these three subsections in one sitting. If you test the commands in the first subsection, retain them for the next subsection and so on. These sections effectively repeat the descriptions shown earlier in this chapter based on command line tools.

# Add an LV

Assume you've added a new hard drive. For the purpose of this section, I'm using the /dev/sda and /dev/sdb drives associated with the baseline virtual machine used for this book. In addition, I've deleted those partitions. That provides up to 2000MB of space