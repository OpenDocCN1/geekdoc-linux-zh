Adding a password=password line in the global options section of your lilo.conf (of course replacing *password* with your password) allows you to protect your system from unauthorized rebooting. Alternatively, you may add a password parameter in each individual stanza to protect certain boot setups differently. For example, you might choose to password-protect the Debian setup but not the Red Hat setup. Typically, the password option is global.

The append line is particularly important. Any parameters that the kernel needs in order to boot correctly can be appended. Typically this line is used to specify parameters for hardware that isn't automatically detected, as in this example. The append line in Listing 3.2 includes the information for an Adaptec 1520B SCSI interface card and a SoundBlaster sound card. Notice that there is no comma between the two append strings, since each one includes commas. Likewise, there are no spaces in each individual append string since the list of strings is space-delimited. The format for these items varies depending upon the item type. Information about hard drives is commonly appended and is specified as follows:

```
append="hd=cccc, hhhh, ssss"  
linear
```

where *cccc* indicates the number of cylinders that the drive has, *hhhh* indicates the number of heads, and *ssss* indicates the number of sectors. You may also use an append line to let LILO know about undetected memory or to test how the system would run with less memory, by indicating less memory than you actually have. The amount of memory can be specified in kilobytes (with a suffix of k) or in megabytes (using a suffix of M). To specify an amount of memory, use the following append line:

```
append="mem=128M"
```

# # The Per-Image Section

The stanzas that follow the global section in Listing 3.2 define two specific Linux kernel images and a bootable Windows partition. For each one, the *image=* line specifies the image or partition location. The *label=* line identifies the name that will be used at the LILO prompt. If *read-only* is included in the stanza, the root file system will be mounted as read-only originally (when it is subject to a file system check); it is remounted read-write later in the boot process. The *root=* line tells where the root directory for the specified kernel is located. Finally, if there is need for an initrd image, its location is specified on a line that begins *initrd=*.

Now let's look at the specific stanzas to understand the differences. The first stanza, with the label *linux*, boots a kernel image located at */boot/vmlinuz-2.4.7-10-1*, initially as read-only. The root partition to use is located at */dev/hdb1*, the boot sector of the first partition of disk 2.

Now, looking at the second stanza, labeled *debian*, we see that it uses the same kernel image, also booted as read-only, but it uses a different root directory and includes an initrd image, as was described in the GRUB section above. The difference in the root partition is because this stanza boots a different Linux installation—specifically, a Debian Linux setup instead of the Red Hat distribution booted with the *linux* stanza. The root files for the Debian distribution are located on the first partition of the third IDE disk, */dev/hdc1*. Since we are using the same kernel in both places, we use an initrd image to change the modular information as appropriate for the Debian distribution.

The fourth stanza points to a Windows 98 installation. This stanza is simpler than the previous three. It doesn't need to contain anything beyond an *other=* line, to specify the path to that operating system's boot sector, and a *label* line, which specifies the name to be input at the LILO prompt to start up that operating system. The information needed to boot Windows is contained in the boot