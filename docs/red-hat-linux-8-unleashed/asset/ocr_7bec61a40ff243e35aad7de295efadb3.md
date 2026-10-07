# CHAPTER 10 Managing the Filesystem

![](bbox=[0.23335, 0.07684999999999999, 0.7393500000000001, 0.40335000000000004])

FIGURE 10.1 the help screen offers a list of partitions and some gentle warnings from fdisk.

Running it with a device name for an argument follows,

```
# sfdisk /dev/sda
```

results in a warning as shown in Figure 10.2

![](bbox=[0.23335, 0.56435, 0.7393500000000001, 0.68935])

FIGURE 10.2 Even given the device name is futile. You must use the -f option to force sfdisk to open the partition table, except more warnings.

Start sfdisk with the -f argument, as shown in Figure 10.3.

The sfdisk utility contains some precautions that will be useful to when you are manipulating the partition table; these precautions warn you of the consequences of what you are asking it to do and force you to consider everything you ask sfdisk to.