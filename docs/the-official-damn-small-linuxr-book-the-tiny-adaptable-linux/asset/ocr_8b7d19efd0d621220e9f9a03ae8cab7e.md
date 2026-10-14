As I mentioned earlier, sometime you need a more capable machine to produce what is needed for the less able machine. We will call the more capable machine the source machine and the other the target machine.

Your source machine needs to be able to boot the DSL CD-ROM, either the Syslinux or Isolinux version, and must also have a floppy drive. You also need a stack of approximately 35 floppies. Make sure these are good—they should have no bad sectors and be in new or new-like condition. You also need the DSL FreeDos Utilities floppy mentioned at the beginning of this chapter.

At the boot prompt of the source machine, enter install. This displays the now familiar DSL installation menu as shown in Figure 8-1.

You have two choices. Depending on the actual size of the DSL release, menu option 8 creates approximately 34 data files. These data files will be named chunk01, chunk02, ... chunk34. Be sure that you have enough space to store an additional 50MB. Using this all-at-once option allows you to copy to floppies at your leisure. These files are not floppy image files like the boot floppies, but instead are data files.

When the process is complete, you will find all of the chunk files. Later, when you have time, you can return to the source computer and manually copy each chunk file to a corresponding floppy disk. Because these are data and not image files, you must first mount the floppy, perform the copy, then unmount the floppy using the umount command.

Alternatively, you may prefer menu option 9. This option creates a chunk and interactively prompts you to insert a blank floppy. This option loops through all chunk files sequentially. Your only interaction is to insert and remove floppies as prompted. This option eliminates all the manual commands needed with option 8. With this option, you need to set aside a good deal of time, but you save much typing.

You may find that you use both options. You may need to recreate a single floppy, and with option 8, you can selectively choose which chunk to copy.

After all the floppies have been created, you might want to take a break. Really, this is a time-consuming endeavor.

To restore all the chunk files on the target machine, boot the target machine with the DSL FreeDOS utilities diskette. Change to the C drive and make the KNOPPIX directory and enter the copy command as shown:

```
A:> c:
C:\> mkdir knoppix
C:\> cd knoppix
C:\KNOPPIX> copy b:\chunk*
```