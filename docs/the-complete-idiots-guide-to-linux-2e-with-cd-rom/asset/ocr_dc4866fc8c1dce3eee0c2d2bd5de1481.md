# dump Examples

The following command will create a level 0 dump (indicated by the 0) on the device specified by the -f flag (in this case /dev/nst0) of the specified disk /dev/hda1 (see /etc/fstab for the name of your disk devices):

```
dump -0u -f /dev/nst0 -s 112778 /dev/hda1
```

Replace nst0 with the appropriate name for your tape device and hda1 with the device used by your root partition. This dump will include all the files found on the device. If you have additional disks, you’ll have to run dump again for each. If you specify the u option and the backup finishes successfully, dump will remember the date, time, and level of this backup. This effectively sets a starting point that can be used to evaluate which files need to be dumped next time.

To create an incremental backup that includes only files modified since the last backup of a lower level, in this case 0, use a higher level dump:

By default, dump writes its output to the default tape unit; you need to remember to specify the -f option followed by the device for your tape drive.

You can redirect the backup to a file using the -f option:

```
dump -9uf /tmp/backup /dev/hda1
```

The preceding command will create a file called backup in the /tmp directory. To redirect the output of dump to STDOUT (standard output), specify a dash (-) instead of a filename:

```
dump -9uf - /dev/hda1 | gzip > /dev/st0
```

In the preceding example, output from dump was sent to STDOUT and piped to the gzip (see Chapter 20, "Installing Programs and Applications") program to be compressed. If your tape doesn’t provide hardware compression, using the preceding command can be an effective way of increasing tape capacity.

For complete information on the myriad of options that dump provides, read your system’s documentation.

# The restore Command