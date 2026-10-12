bc-1.0.10.i386.rpm command specifies a package file, so it needs a -p option, and it wouldn't check installed packages. The rpm -qa | grep "mysql" command will list all installed packages with "mysql" in their package names, but it won't list the files contained in any of those packages.

+   7. The **redhat-config-packages** tool is a package manager that works in both desktop environments.

+   8. From the Red Hat menu, select System Settings, then Packages to run the tool without resorting to the command line.

+   9. Not to be too obvious, but http://www.redhat.com is one place to start. You can also look at http://www.rpmfind.net, http://freshrpms.net, http://www.linuxapps.com, http://freshmeat.net, and others.

+   10. A tarball is a single-file, compressed archive of one or (usually) more files and directories. The **tar** command is used to create the archive, which can be compressed using several different compression utilities.

+   11. Tarballs usually use one of the following extensions: **.tar.gz** or **.tgz** for a gzipped tar archive, or **.tar.bz2** for a bzip2-compressed tar archive.

+   12. The **configure** script often recognizes the --help argument as a cry for help with the available options, so use, **./configure --help**. You could also look at the contents of the **.configure** file using a text editor or even **more .configure**.

+   13. Only the root user can manipulate files in **/usr/local/src** unless you change its permissions, which means you have to copy, configure, and build software as **root**, which shouldn't be necessary and isn't always wise.

+   14. The correct answer is **D**. First run the configure script, then make the software, install it, and clean up afterward.

+   15. Use the **echo $PATH** command to see what directories are in the current path.

+   16. Use the **rm -rf** command to delete a directory and all its subdirectories and all their contents. It's like a nuclear weapon for directories, so be careful!

# Module 5: Managing Users

+   1. A GID is a group ID, which is a unique identifier assigned to each user group.

+   2. A UID is a user ID, a unique numeric identifier assigned to each user account.

+   3. The MD5 encryption scheme can (and should) be installed on Red Hat Linux 8.0 systems.

+   4. The /etc/shadow file contains the MD5-encrypted passwords for the system.

+   5. On a properly configured system, only the root user can view the contents of the /etc/shadow file.

+   6. I suggest adding the asterisk (*) character to the password field to disable login. Furthermore, I suggest adding a brief text description of the reason the password was disabled.