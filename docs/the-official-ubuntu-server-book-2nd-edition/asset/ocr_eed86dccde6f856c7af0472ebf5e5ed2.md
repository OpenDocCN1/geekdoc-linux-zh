# Extra vmbuilder Options

The example vmbuilder command I gave will certainly work, but the script supports a large number of additional options that might be useful for your VMs. For instance, in my example I list the --rootsize and --swap size options to set the root and swap partitions in my VM's disk. You might decide that you want a more complex partition layout than just a root and swap partition, in which case you can use the --part option. The --part option reads from a file you create that contains partition information and uses it when it sets up disks. The file has a very basic syntax. Each line contains a mount point followed by a partition size in megabytes. You can even set up multiple disks—just use --- on its own line to separate one disk from another.

For instance, let's say I wanted to create two disks. The first disk would have a 100Mb /boot partition, a 2Gb / partition, and a 512Mb swap. The second disk would have a 5Gb /var partition. I could create a file called test1.partitions containing the following data:

```
/boot 100
root 2000
swap 512
---
/var 5000
```

Now when I run vm-builder I replace the --root 2000 --swap 256 lines in my command with --part /path/to/test1.partitions. The final command would look like this:

```
$ sudo vmbuilder kvm ubuntu --suite lucid --flavour virtual
--arch i386 --hostname test1 --libvirt qemu:///system
--part /home/ubuntu/vminfo/test1.partitions --user ubuntu
--pass insecure -d test1-kvm
```

# Package Management

The vmbuilder script also has a number of handy preseed-like options for automating your install. Here are some options specifically aimed at package management:

+   --addpkg packagename and --removepkg packagename

The --addpkg and --removepkg commands will respectively add and remove a package you specify as an argument. You can add multiple