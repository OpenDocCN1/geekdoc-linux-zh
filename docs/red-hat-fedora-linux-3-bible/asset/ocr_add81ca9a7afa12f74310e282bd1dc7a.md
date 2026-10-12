| | | |
|---|---|---|
| -h | | If this option is specified, restore re-creates directories marked for extraction but will not extract their contents. |
| -m | | Files are extracted by inode number instead of name. This is generally not very useful. |
| -N | | Instead of extracting files, print their names. |
| -s file# | | Specify the dump file to start with on a multiple file tape. This takes a numeric argument. |
| -T directory | | Tells restore where to write any temporary files. This is useful if you booted from a floppy disk (which has no space for temporary files). |
| -v | | Run in verbose mode. This causes restore to print information about each file as it restores it. |
| -Y | | The restore command will always continue when it encounters a bad block, rather than asking you if you want to continue. |

# ## Restoring an entire file system

Let's return to our earlier example of the Friday disk crash. You installed a shiny new hard drive and your backup tapes are in hand. It is time to restore the files. For the purpose of this example, I assume that the crashed drive contained only the /home partition and that the Fedora Linux operating system is still intact. If the crashed disk had contained the Fedora Linux operating system, you would first have to reinstall Fedora Linux before restoring the backup.

Before any files can be recovered to your new hard drive, an empty file system must be created on it. You use the mkfs command to do this. The mkfs command can accept a variety of parameters, but usually you only need to supply the name of the device to create the file system on. Thus, to prepare the new hard drive, type:

```
`# mkfs -t ext3 /dev/hda6`
```

Alternatively, because your /home drive is listed in the /etc/fstab file, you can simply specify the /home mountpoint and mkfs will figure out the correct device. Thus, the preceding command could be replaced with this:

```
`# mkfs /home`
```

> > **CAUTION:** You should, of course, exercise extreme caution when using the mkfs command. If you specify the wrong device name, you could unintentionally wipe out all data on an existing file system.

After creating a file system on your new disk, mount the partition to a temporary mount point.

```
`# mkdir /mnt/test` `
` `# mount /dev/hda6 /mnt/test`
```