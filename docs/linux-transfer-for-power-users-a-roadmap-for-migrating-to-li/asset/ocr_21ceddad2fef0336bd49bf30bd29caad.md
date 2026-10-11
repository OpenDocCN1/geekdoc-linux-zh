# /sbin

/sbin contains utilities used for system administration. Programs that are involved with booting the machine as well as repairing broken installations and recovering corrupt files are located here. There is also a /sbin directory under /usr, called /usr/sbin, that contains similar programs that are executed after /usr has been mounted during boot up.

# /tmp

/tmp is reserved for programs that create or use temporary files, just like C:\temp (or C:\Documents and Settings\<user>) in Windows. Note that the contents of /tmp are deleted during the boot process, so don’t ever expect something in /tmp to be there five minutes later.

# /usr

/usr is roughly equivalent to “Program Files” in Windows. It has six major subdirectories.

/usr/bin contains programs used by regular users of the system that are not in /bin. /usr/include and /usr/lib contain libraries that aren’t found in /lib. /usr/local is empty after initial installation, but eventually gets populated with programs installed by users. /usr/sbin has been covered in the /sbin description. /usr/share is used for data that isn’t modified once created. For example, a program that creates a key or other type of fingerprint file might put it in /usr/share/<program>.

# /var

By now you’re probably getting used to the abbreviations—and so it comes as no surprise that /var is used for variable data files. Examples include mail and print spoolers, log files, lock files, temporary files saved during system reboots, and caches for specific applications.

# Which ones are important?

These are brief descriptions of these folders. You can find more precise definitions and detailed information about subdirectories of these folders, at http://www.pathname.com/fhs.

You’ll see that some distributions, such as Fedora Core, include other top-level directories, such as /libboot. Don’t worry about them.

So now that we’ve been through the definitions, which ones are important? You can use Linux for a long time while dealing with only three directories: /home, /etc, and /usr. If pressed, you might be interested in /bin, /sbin, /tmp, and /var.

If you’re using a different distribution, you’ll find many of these directories are the same as found in other distributions; in fact, the differences are fairly minor—much like the differences you find between the directory structures of Windows 95 and Windows NT, for example, where the directory “Windows” was changed to “WINNT” (and then back again in Windows XP, ahem!).

# About multiple drives

During the conversation in the previous section, I quickly skipped past the “Where’s my C: drive?” issue and just talked about the folder structure under the “/” folder. If you’ve got a single hard disk, you can just assume that “/” sits on that hard drive much like “C:” would, and accept that you’ll find your floppy and CD-ROM drives under /mnt. But what if you’ve got more than one hard disk? What does the tree structure of folders look like in that case?

The answer: Exactly the same!