# Disk Heights

The preceding discussion omitted mention of the height of various drive types. This is because each of the disk varieties comes in an assortment of heights.

+   • 2.5-inch drives are available in heights ranging from 0.33 inch to 0.492 inch, to fit an
+   assortment of notebook computer sizes.

+   • 3.5-inch drives are most commonly available in third-height form, which is 1.02 inches.
+   A few half-height (1.64 inch) models are also available. Typically, the highest-capacity
+   drives in a model line fit the half-height form factor, whereas small- and medium-
+   capacity drives come in third-height form.

+   • 5.25-inch drives typically come in half-height form (1.64 inch), although a few ancient
+   full-height behemoths measure more than 3 inches in height.

Be sure to check on the height of any drive before you buy it, particularly if you’re low on expansion bays. If you buy a half-height 3.5-inch drive but don’t have room for it in your case, you’ll have to return the drive, remove some other component, or use an external drive housing to add the drive to your system. Your options are even more limited if you buy a 2.5-inch drive to replace a notebook computer’s built-in drive.

# Tuning Disk Performance in Linux

You probably want to get the best performance possible from your hard disks. If you have a hard drive capable of transferring 30MBps, you don’t want to get only 8MBps speeds from it. Especially when using a laptop computer, you also want to configure your hard drives to *spin* *down* when not being actively used—that is, to go into an inactive state in which the hard disk platters don’t spin, but the drive watches for data transfer requests and powers up the drive when one occurs. You can use an assortment of Linux utilities and configuration features to help improve your overall system performance with respect to hard disks.

# Using hdparm to Activate Advanced Features

The most important Linux utility for handling advanced hard disk features is `hdparm`. This utility lets you set an assortment of options relating to hard disk performance, as well as run tests to find out how your hard disk is performing. You can learn more about `hdparm` by typing `man` `hdparm`. I present some highlights here.

> NOTE

You must be running as root to use most of `hdparm`’s features.