# mkswap

If you want to create a swap partition, you first use `fdisk` or `parted` to create the partition, if it does not already exist, and then you use the `mkswap` command to format it as a swap partition. `mkswap` formats the entire partition unless otherwise instructed. It takes as its argument the device name for the swap partition.

```
mkswap /dev/hdb2
```

You then need to create an entry for it in the `/etc/fstab` file so that it will be automatically mounted when your system boots.