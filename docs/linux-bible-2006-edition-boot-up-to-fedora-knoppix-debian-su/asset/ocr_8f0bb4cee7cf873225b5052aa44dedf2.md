assign your KNOPPIX home directory (/home/knoppix) to use some of the available space on your hard drive. That can be done in two ways:

+   * Assigning an entire partition to be used for your home directory.
* Assigning a part of that for your home directory, in the form of an image file.

You can also put your persistent home directory on rewritable, removable media, such as a memory stick. Once you create that area to use as your home directory, you can tell KNOPPIX it every time you restart KNOPPIX. Here's what you do:

+   1. Click the squished penguin in the panel, and then Select Create Persistent KNOPPIX disk image. A window appears, asking if you are ready to create a persistent home directory.
2. Click Yes to continue. You are asked which partition you want to use for your persistent home directory.
3. Select the partition you want to store your persistent desktop and click OK. You are asked if you want to save the home directory in an encrypted format.
4. Select No, to have the directory encrypted (if you choose Yes, you'll have to specify a password that you will need to access the persistent home directory at boot time). You are asked to enter the size of your home directory.

+   5. Type the number of megabytes to assign to your home directory and click OK. Be sure that much space is available on the partition. (When the partition is mounted, you can use df -h to see how much space is available on it.) The partition or image file should be created.

When I ran this procedure to create a 100MB image over the hd5 partition, the file /mnt/hd5/knoppix, img, which had 97MB of available space. To see how to use that, see the "Restarting KNOPPIX" section later in this chapter.

# Keeping Your KNOPPIX Configuration

After you have gone through all the work to configure your setup, printer, network, disks, and other preferences for your it's a shame to lose all that on your next reboot. Well, KNOPPIX offers a way that you can save your configuration information and reuse it for your next session. Saved information can be stored on a floppy disk or any other medium that is accessible (as your hard disk) the next time you reboot KNOPPIX. Here's how:

+   1. From the squished penguin icon on the panel, click Configure- Save KNOPPIX configuration.