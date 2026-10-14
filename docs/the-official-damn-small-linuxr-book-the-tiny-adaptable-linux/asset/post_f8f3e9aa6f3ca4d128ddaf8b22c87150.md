
## FIGURE S-15
Web extension selection screen.

![](img/af53325d7f38f1cdafca9f44568e4ab8_132_0.png)

3. Click the info link in the Info column to see the extension’s info page, as described in the automated process. This step is critical. You should always read the info file. Use the back arrow to return to the available extensions.

4. Right-click the extension name link in the Application column (third column from the right), then select the Save Link As item in the browser’s submenu.

## NOTE

We do not recommend downloading MyDSL extensions to your home directory. MyDSL extensions are large and static. The fact that DSL is used primarily as a live CD, or emulation thereof, implies that a backup/restore is required for saving personal settings. Having large static—that is, non-changing—items in your backup only slow down your system. Or worse, they cause your backup to fail as it may become too large for the chosen backup device. It is best to have a persistent store for collection of MyDSL extensions.

So far, this is all fairly standard for downloading files via a browser. However, there are pitfalls to be aware of. Don’t forget to read those info files. Many times an extension requires additional extensions or may have special instructions. Many questions arise from failure to perform the extra step to read the extensions’ info file.

5. Right-click the md5sum link corresponding to your selection. After it has downloaded both the extension and the corresponding md5.txt to the same directory, you must manually verify that you indeed have a valid download. To do this, use the command

```
$ md5sum -c extension_name.ext.md5.txt
```

The extension_name.ext is replaced by the name of the extension you downloaded. You should see OK as the result. If not, you must redownload until the extension can be validated by its checksums.

All of these extra and manual steps can be avoided by using our automated GUI download system.

## SAVING YOUR EXTENSIONS

Because DSL was created as a nomadic guest operating system, no drives or devices are automatically mounted. In fact, the default user dsl does not have administrator privileges to have write access to physical devices. The default for using the MyDSL system is to download the extensions to /tmp, which resides on the RAM disk (/ramdisk).

After downloading and trying the extension, you most likely want to keep it. Recall that MyDSL extensions were built with the live CD user in mind. Therefore, upon a reboot or shutdown, the extensions are gone.

Having a persistent store for your favorite extensions means you must mount a drive and copy the extensions to that location. There are many ways to accomplish this task:

- File manager—Using one of the file managers to save files is discussed in Chapter 3, "Using DSL Applications." For this task, you have to select the root version of the appropriate file manager.
- Save during shutdown—I did provide a sort of safety net upon shutdown. If you have any extensions still residing on the RAM disk-based /tmp directory, a dialog prompts you to save them. If you select OK, the system file manager emelfm opens with root privileges to allow you to save your extensions.

Remember that you can use the mounting tool in the lower-right corner of the DSL desktop to mount the partition from your hard disk or pen drive where you want to install the extension.

## Boot Time Automatic Extension Loading

Because you save your extensions in their packaged form to a persistent store, you must specify how they are to be loaded upon your next boot.

MyDSL extensions install automatically during the boot process, either by placing them in a location which is searched by default or by placing them in a directory of your choice and using the boot time option myds1=location, where location can be the Linux device name. For example, myds1=hda1 or myds1=sda1 represents the first partition on your first IDE hard disk or SCSI hard disk (or pen drive), respectively. The location can even include a full path to the directory (such as myds1=hda1/myds1).

First, let’s discuss the default locations for DSL. By using a default, you do not need a boot time option and therefore can have a hands-free boot up.

- On the boot disc—The first default location is the top level of your DSL installation. This top level, whether it be a mkmyDSL CD (discussed in Chapter 11) or an on emulation type install (discussed in Chapter 8, “Installing DSL in Alternate Ways”), is to place your extensions where the /KNOPPIX and /boot directories are located.
- On attached storage devices—The second default location is in a directory named myds1 in the top level of each available attached device.

Using either of these two default specifications means you do not need to use a boot option. The system scans each available drive device looking for a myds1 directory.

> NOTE
> Specifying the device name can have faster boot times. You don’t get the hands-free boot, but it also means that the system does not have to scan drives looking for a myds1 directory.

In DSL version 1.2, I introduced the capability to specify a directory of your choice for mydsl extensions. This can be useful if you have multiple sets of applications and want to choose which set to load for any given session.

For example, you can put your extensions in a directory called /mnt/hda2/games and use the boot option myds1=hda2/games. You can even have multiple setups. Have another collection of extensions in a directory called /mnt/hda2/office. Then, at boot time, decide to play games or work. This type of flexibility helps save resources on low RAM machines. Remember, everything we
