+   2. Create the etc directory (usr/ftp/etc, for example) and copy your passwd file (/etc/passwd) and group file (/etc/group) into it. We’ll edit these files in a moment.

+   3. Create the lib directory (/usr/ftp/lib, for example) and copy the files /lib/ld.so and /lib/libc.so.X (where X is the version number of the libc file) into it. These files are used by ls. Do this step only if your ls command requires these files; most versions of Linux do not have this dependency.

+   4. Create the pub directory (/usr/ftp/pub, for example) to hold your accessible files. We’ll look at this directory in more detail in a moment.

+   5. Create the dev directory (/usr/ftp/dev, for example) and use the mknod command to copy the /dev/zero file. You need to retain the same major and minor device numbers as the /dev/zero file in /dev. This device file is used by ld.so (and hence ls). Do this step only if ls requires the /lib directory files mentioned earlier.

The copies of the /etc/passwd and /etc/group files are copied into the ~ftp/etc directory. You should edit these files to remove all passwords and replace them with an asterisk. Remove all entries in both /etc/passwd and /etc/group, except those used by the anonymous FTP login (usually just anonymous and bin).

The ~ftp/pub directory structure can be used to store the files you want to allow anonymous users to access. Copy them into this directory. You can create subdirectories as you need them for organizational purposes. It may be useful to create an upload directory somewhere in the ~ftp/pub directory structure that has write permission, so that users can upload files to you only into this upload area.

> **NOTE**

If you allow remote users to access your system, you may want to protect yourself legally by issuing a warning that their activities on your system may be recorded or logged. Unfortunately, in today’s world you have to take all steps necessary to prevent getting sued!

# Setting Permissions

You can use the chroot command to help protect your system. The chroot command makes the root directory appear to be something other than / on a file system. For example, since chroot is always set for the anonymous FTP login, any time anonymous users type a cd command, it can always be relative to their home directory. In other