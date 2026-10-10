# ### Scope of Task

This task requires editing a single configuration file, /etc/fstab. To test that your changes work, you'll need to use the mount command both as root and as an ordinary user.

# ### Duration

This task should take about half an hour to complete. Once you're familiar with it, making simple changes to the /etc/fstab file will take just a few seconds, and testing them will take a few seconds more. If you need to gather data such as filesystem type codes or add hardware, though, total modification times can stretch into several minutes.

# ## Setup

You'll need access to the disk you used in Task 5.3, so be sure it's installed and ready. To add the NFS server and Zip disk entries, you'll need access to an NFS server and a Zip disk. If you don't have these things, you should simply read the relevant descriptions. Most of this task requires root access, so you should log in and acquire superuser privileges.

# ## Caveats

The usual cautions concerning working as root apply to this task. Furthermore, the /etc/fstab file is a critical system configuration file. If you accidentally delete or change a line, you could cause problems ranging from subtle and minor problems on relatively unimportant filesystems to rendering your system unbootable.

![](bbox=[0.135, 0.548, 0.856, 0.605])

# ### Procedure

To perform this task, you must add four lines to your /etc/fstab file, one for each of the three filesystems and one swap partition you want to configure. Before you begin, though, you should familiarize yourself with the file format used by /etc/fstab.

# ### Understanding the /etc/fstab File Format

The /etc/fstab file consists of a series of lines that contain six fields each; the fields are separated by one or more spaces or tabs. A line that begins with a hash mark (#) is a comment and is ignored. Listing 5.1 shows a sample /etc/fstab file.

# **Listing 5.1: Sample /etc/fstab File**

```
#device mount point filesystem options dump fscx
/dev/hda1 / ext3 defaults 1 1
```