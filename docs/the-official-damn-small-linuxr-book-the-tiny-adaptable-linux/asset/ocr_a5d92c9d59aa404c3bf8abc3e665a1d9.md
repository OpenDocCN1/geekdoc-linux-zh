# Boot Time Automatic Extension Loading

Because you save your extensions in their packaged form to a persistent store, you must specify how they are to be loaded upon your next boot.

MyDSL extensions install automatically during the boot process, either by placing them in a location which is searched by default or by placing them in a directory of your choice and using the boot time option myds1=location, where location can be the Linux device name. For example, myds1=hda1 or myds1=sda1 represents the first partition on your first IDE hard disk or SCSI hard disk (or pen drive), respectively. The location can even include a full path to the directory (such as myds1=hda1/myds1).

First, let’s discuss the default locations for DSL. By using a default, you do not need a boot time option and therefore can have a hands-free boot up.

+   On the boot disc—The first default location is the top level of your DSL installation. This top level, whether it be a mkmyDSL CD (discussed in Chapter 11) or an on emulation type install (discussed in Chapter 8, “Installing DSL in Alternate Ways”), is to place your extensions where the /KNOPPIX and /boot directories are located.

+   On attached storage devices—The second default location is in a directory named myds1 in the top level of each available attached device.

Using either of these two default specifications means you do not need to use a boot option. The system scans each available drive device looking for a myds1 directory.

> NOTE
> Specifying the device name can have faster boot times. You don’t get the hands-free boot, but it also means that the system does not have to scan drives looking for a myds1 directory.

In DSL version 1.2, I introduced the capability to specify a directory of your choice for mydsl extensions. This can be useful if you have multiple sets of applications and want to choose which set to load for any given session.

For example, you can put your extensions in a directory called /mnt/hda2/games and use the boot option myds1=hda2/games. You can even have multiple setups. Have another collection of extensions in a directory called /mnt/hda2/office. Then, at boot time, decide to play games or work. This type of flexibility helps save resources on low RAM machines. Remember, everything we