# FIGURE 6.5
A CD-ROM's contents
as they appear in a CDE window

![](bbox=[0.22, 0.12, 0.88, 0.48])

Alternatively, you can use the list (ls) command to obtain a directory listing of a CD-ROM's contents from the command line. The syntax for this command for CD-ROM1 is as follows:

```
ls -L [-1] /cdrom/cdrom0
```

The -L tells the list command to list the symbolic links, and -1 specifies the long format listing that includes both permissions and owners. Figure 6.6 shows the list command's output for the CD-ROM whose contents were shown in Figure 6.5.

To access a CD over the network, you must first create a directory and then mount it. Do the following:

+   1. Enter the `mkdir <directory>` command at the command line to create a directory name that will be the mount point for the CD.
+   2. Find the name of the CD you want to mount by entering the first line of the following:
+   
+   ```shell
+   showmount -e system-name
+   export list for system-name
+   /cdrom/sol_8_sparc
+   ```
+   3. Log in as superuser (if needed) by entering first `su`, then the su's password.
+   4. Then mount the CD-ROM using the following command:
+   
+   ```shell
+   # mount -F nfs -o ro <system-name>:/cdrom/<cd-name>\
+     <local-mount-point>
+   ```