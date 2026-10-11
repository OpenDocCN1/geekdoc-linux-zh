```
Loading Ramdisk..........
```

Some other information then appears as the drivers are loading. The next time the text stops, you see the following:

```
VFS: Insert root floppy disk to be loaded into ramdisk and press ENTER
```

Remove the boot disk and replace it with the root disk using **color.gz** (or whichever root package you picked), and then press enter. You will see another welcome message and a prompt. At the prompt, type root without quotes. Like this:

```
Slackware login: root
```

You won't be prompted for a password. After you've logged on, you get a prompt that looks like this:

```
#
```

This is the prompt for the root account, meaning you have total control of the system. As soon as you get the prompt, format your partition for Linux.

![](bbox=[0.08, 0.495, 0.18, 0.585])

Be careful not to overwrite your other operating systems partitions by deleting them or formatting them.

To format your disk, use the Linux command **fdisk**.

![](bbox=[0.08, 0.675, 0.18, 0.765])

Remember: issue the **fdisk** command from the Linux side, not from the DOS or Windows partition. You may have encountered the DOS disk command before, but this is not the same program!

To run **fdisk**, type **fdisk** at the root prompt so it looks like this:

```
# fdisk
```

Then you will see the following lines:

```
Using /dev/hda as default device!
Command (m for help):
```