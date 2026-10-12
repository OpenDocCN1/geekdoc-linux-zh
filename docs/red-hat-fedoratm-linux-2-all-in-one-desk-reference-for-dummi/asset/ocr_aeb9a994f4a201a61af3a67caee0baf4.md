2. Kudzu detects the USB storage device and adds an entry in `/etc/fstab` that associates the USB device with the mount point `/mnt/flash`. Mount the device with the command:

```
mount /mnt/flash
```

3. To check that the USB device is mounted, type the following command and look for a line in the output that shows `/mnt/flash`:

```
df
```

For example, the following line of output is for a 32MB USB keychain device:

```
/dev/sda1 31520 64 31456 1% /mnt/flash
```

If you don't have any other USB device plugged in, the device name is `/dev/sda1` (USB storage devices appear as SCSI devices). The next USB storage devices gets the `/dev/sda2` device name and so on.

Now you can access the files on the keychain at the `/mnt/flash` directory. To save a file to the USB keychain storage device, use a command of the following form:

```
cp filename /mnt/flash
```

where *filename* is the name of the file you want to save.

When you're done using the device, unmount the USB keychain with this command:

```
mount /dev/sda1
```

That's it!

# # Managing Print Queues in Fedora Core

PCs typically come with one parallel port, typically used to connect the printer to the PC. You can set up a printer fairly easily by using Fedora Core's graphical printer-configuration utility, but you also have to know how to manage the print queue.

# ## Spooling and print jobs

*Spooling* refers to the capability to print in the background. When you print from a word processor in Windows, for example, the output first goes to a file on the disk. Then, while you continue working with the word processor, a background process sends that output to the printer. The Fedora Core printing environment also supports spooling.