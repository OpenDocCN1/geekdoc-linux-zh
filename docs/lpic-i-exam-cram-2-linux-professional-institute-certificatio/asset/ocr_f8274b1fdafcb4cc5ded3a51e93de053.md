+   - stats—Shows the statistics for the file system and is similar to the dumefs -h output
+   - ls—Shows the directory, which by default is the root ( / )
+   - pwd—Shows the working directory
+   - undelete—Undeletes a file (used immediately after the deletion in successful cases)
+   - logdump—Shows the contents of the journal (if in a journal-led file system)
+   - quit—Quits the tool

# ## Mounting and Unmounting

In the final section of this chapter, we will discuss mounting and unmounting file systems, the options available, and how this subject is used for the exam.

# ## The File System Table

For a file system to be used by normal users, that file system must either be mounted by the root user or be put in the /etc/fstab file with the correct options that allow users that privilege. When a proper entry exists in the /etc/fstab, a user only needs to issue the mount command with the full path of a mount point or device to accomplish the mount.

File systems should be set up in /etc/fstab, one per line. Entries that are mounted are reflected in /etc/mtab, which is maintained by the system as a description of the mounted file systems. This information (or most of it) is also in the /proc/mounts file.

Type the mount command to see the current list of file systems. Here’s an example:

```
```
mount
/dev/sda2 on / type ext3 (rw)
none on /proc type proc (rw)
usbdevfs on /proc/bus/usb type usbdevfs (rw)
/dev/sda1 on /boot type ext3 (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
/dev/sdb8 on /home/data type ext3 (rw)
```
```