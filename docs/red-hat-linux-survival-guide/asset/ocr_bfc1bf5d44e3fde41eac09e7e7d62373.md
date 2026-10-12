Your anonftp package name varies based on your system architecture and anonftp version. Also note that the anonftp package does not install if you don't already have an FTP server such as wu-ftpd.

# Step 4: Copy the anonftp package files to the guest user’s home directory

Change directory to ~ftp and use the following command to copy all the files and directories to, for example, ~mrfrog:

```
tar cvf - * | ( cd ~mrfrog ; tar xvf - )
```

All mrfrog really needs are the ~ftp/bin, ~ftp/etc, and ~ftp/lib directories. You can delete the ~ftp/pub directory or any other directory from your ~ftp directory.

# Step 5: Update the ~mrfrog/etc/passwd and ~mrfrog/etc/group files

Now edit the ~mrfrog/etc/passwd file and remove the line for the ftp user. Append the exact password line for mrfrog from the /etc/passwd file. However, remove mrfrog’s password and replace it with a * to make it invalid. For example:

```
mrfrog:1dev33vylewv.:516:519::/home/mrfrog/./:/bin/true
```

Copy this line to ~mrfrog/etc/passwd and replace the password so that the line looks like the following:

```
mrfrog:*:516:519::/home/mrfrog/./:/bin/true
```

Now, modify the ~mrfrog/etc/group file and add the mrfrog line found in /etc/group.

![](bbox=[0.06, 0.83, 0.17, 0.91])

I assume that you have not somehow disabled Red Hat's default feature for automatic creation of a private group by the same name as the new user. In other words, when you create a user with the useradd program, it automatically creates a private group for that user with the same name. So when you