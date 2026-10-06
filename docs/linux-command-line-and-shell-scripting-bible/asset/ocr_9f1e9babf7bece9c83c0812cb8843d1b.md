# The Linux Command Line

When changing the name of a group, the GID and group members remain the same, only the group name changes. All security permissions are based on the GID, you can change the name of a group as often as you wish without adversely affecting file security.

# Decoding File Permissions

Now that you know users and groups, it's time to decode the cryptic file permissions you've seen when using the `ls` command. This section describes how to decipher the permissions and where they come from.

# Using file permission symbols

If you remember from Chapter 3, the `ls` command allows us to see the file permissions for files, directories, and devices on the Linux system:

```
$ ls -l
total 68
-rw-rw-r-- 1 rich rich 50 2007-09-13 07:49 file1.gz
-rw-rw-r-- 1 rich rich 23 2007-09-13 07:50 file2
-rw-rw-r-- 1 rich rich 48 2007-09-13 07:56 file3
-rw-rw-r-- 1 rich rich 34 2007-09-13 08:59 file4
-drwxr-xr-x 1 rich rich 4096 2007-09-18 13:58 myprog
-drwxr-xr-x 1 rich rich 237 2007-09-18 13:58 myprog.c
-drwxrwxrxr-x 2 rich rich 4096 2007-09-03 15:12 test1
-drwxrwxrxr-x 2 rich rich 4096 2007-09-03 15:12 test2
$
```

The first field in the output listing is a code that describes the permissions for the files and directories. The first character in the field defines the type of the object:

+   - for files
- d for directories
- l for links
- c for character devices
- b for block devices
- n for network devices

After that, there are three sets of three characters. Each set of three characters defines an access triplet:

+   - r for read permission for the object
- w for write permission for the object
- x for execute permission for the object