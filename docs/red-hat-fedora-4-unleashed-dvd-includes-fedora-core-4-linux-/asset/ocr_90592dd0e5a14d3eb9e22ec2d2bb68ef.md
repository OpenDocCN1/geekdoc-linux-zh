*Special devices* are block or character devices established for a special purpose. Two special devices of interest are

+   - `/dev/null`—This is the null device, also called the “bit bucket.” Any output written to it is discarded. It is useful to redirect messages to it when you do not want them displayed on the standard output or written to a file. For example,
+   	`$ ls 2> /dev/null`

will display the file listing to the screen, but will not display any error messages even though the `ls` command might generate one; we redirected the standard error messages (`2>` ) to `/dev/null`. Almost all commands generate messages to the standard output and standard error when run, and sometimes, as when running a script, it is useful to not see the messages.

+   - `/dev/zero`—This device has an inexhaustible supply of zeros; use all you want—it makes more. It is very useful for writing strings of zeros to a device or file, such as when preparing an image of a file system (perhaps to be copied onto compact flash or other media).

# ## Naming Conventions Used for Block and Character Devices

The traditional naming system for block and character devices has been in use for a while. In `/usr/src/linux-2.6/Documentation/devices.txt`, the device name for the first partition of the first IDE disk would be `/dev/hda1`. If it were a SCSI disk, it would be `/dev/sda1` (shown elsewhere in `devices.txt` file).

All device names are included in `devices.txt`, and all the devices that have been created on your system are listed in the `/dev` directory. That directory also can hold links; for example, `/dev/cdrom` can actually be a link back to the actual device that is your CD-ROM (perhaps `/dev/hdc?` or `/dev/srd0?` ). `/dev/mouse` and `/dev/modem` are commonly used symbolic links in the `/dev` directory.

# ## Using mknod to Create Devices

If you need a device file in `/dev` that’s not already there for some reason, you can create the special file with the `mknod` command. You might have noticed that `/dev` lists devices that you do not have. That’s because the device’s listing must appear in `/dev` before the system can use the actual device; if you install the hardware at some point in the future, the system will not create the device files on-the-fly. So, if you’re preparing to install a device, and you check `/dev` but find that it does not contain the device’s file, you can create the file with `mknod`.

Creating files with `mknod` is a straightforward process as long as you know what type of device you are creating the file for and what the device’s major and minor numbers are.

```
```
# mknod [OPTION]… NAME TYPE [MAJOR MINOR]
```
```