# XFree86 and TGA

If you have an Alpha with a TGA card and you choose to install XFree86, the installation program prompts you to choose a video card. Choose Unlisted Server; the installation program displays a list of available servers. Choose the TGA server.

# 3.6.4  Finishing Up

After the install is finished and your system is fully configured, you will be asked to reset your computer. This indicates that your system has been successfully installed.

# 3.7  Booting your Red Hat Linux/Alpha system

To boot Red Hat Linux from MILO, you must use the boot command. The command differs slightly depending on where your root partition is. For example, if your root partition is the second partition on your first SCSI hard drive, you would boot as follows:

```
boot sda2:vmlinux.gz root=/dev/sda2
```

If instead your root partition is the third partition on your second IDE drive, you would use this command:

```
boot hdb3:vmlinux.gz root=/dev/hdb3
```

For information on these commands and on automating the boot process, please read the MILO HOWTO in Appendix D.