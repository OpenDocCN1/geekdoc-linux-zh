# Boot Management CHAPTER 49

| /dev/hdc 592892 592892 0 100% /mnt/cdrom |
| /dev/fd0 1423 57 1366 4% /mnt/floppy |

Armed with your information, you are now ready to edit LILO's configuration file,
/etc/lilo.conf.

# Editing lilo.conf

Editing lilo.conf is easy. Make sure you're logged in as root and load the file into your
favorite editor, making sure to save your changes and save the file as ASCII text. You
edit lilo.conf for a number of reasons:

+   - You are testing a new kernel and want to be able to boot the same Linux partition
 more than one kernel. This is done by using multiple entries of the image =
section of lilo.conf. You may have multiple kernels installed on your Linux
partition and boot to a different kernel by typing its name (specified in the
section).
 You want to add password protection to a partition.
- You have a hardware setup that requires you to specify special options, such as
boot a remote filesystem.
- Your kernel is called something other than /mlinuz or is in a nonstandard place,
such as /etc.

![](bbox=[0.873, 0.452, 0.951, 0.603])

List 3.1 shows a sample lilo.conf file (displayed by the YaST command). In this
configuration, two different Linux distributions may be booted.

> Note
Need more information about configuring LILO? Don't overlook Cameron
Spitzer's mini-HOWTO named LILO under the /usr/doc/howto/en/mini directory.
You'll find additional troubleshooting tips on how to configure your
lilo.conf file.

# LISTING 3.1 A yast-generated lilo.conf

```
# LILO Konfiguration-Datei
# Start LILO global Section
boot=/dev/hda
#compact # faster, but won't work on all systems.
vga = normal # force sane state
```