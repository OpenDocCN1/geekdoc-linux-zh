
Because you don't have read access to the ~/ftp/incoming directory, you shouldn't be able to see the files you upload using the ls command. However, you still can download the uploaded files if you supply the proper filenames.

## Enhancing anonymous FTP security

Creating an anonymous FTP site is already a security risk, and having an uploadable directory increases that risk. However, many organizations have successfully run anonymous FTP servers for years, so don't be extremely discouraged—just be cautious. Here are some guidelines for enhancing anonymous FTP server security:

- Ensure that the ftp account in /etc/passwd is using an invalid password. For example, your ftp account entry in the passwd file should look like this:
  `ftp:*::14:50:FTP User:/home/ftp:/bin/true`
- The ~/ftp/bin directory should be owned by root and not by the ftp account. The binaries, such as ls, compress, and tar, that you have in the ~/ftp/bin directory also must be owned by the root user. The ~/ftp/bin directory and its contents should be executable only. Run the following to ensure that all files in the ~/ftp/bin directory are executable only:
  `chown -R root.root ~/ftp/bin; chmod -R 111 ~/ftp/bin`
- The ~/ftp/etc directory should be owned by the root user, and it must be executable only. You can make it so by using the following commands:
  `chown -R root.root ~/ftp/etc; chmod 111 ~/ftp/etc`
- Contents of the ~/ftp/etc directory must be read-only and must be owned by root. Run the following to make sure the permissions are set up correctly:
  `chown -R root.root ~/ftp/etc; cd ~/ftp/etc; chmod 444 *`
- Never copy your /etc/passwd or /etc/group files into the ~/ftp/etc directory. The ~/ftp/etc/passwd and ~/ftp/etc/group files are dummy files needed to satisfy programs that look for them when running under ~ftp as the root directory because of the server's chroot to ~ftp.
- As a general security rule, make sure that no files or directories in ~ftp are owned by the ftp user.

## Creating a guest FTP account

A guest FTP account is a real account with a real username and password. When a guest user logs in to an FTP server, the server does a chroot operation to the guest user's home directory, thus making the home directory of the guest user appear as the entire file system.

The easiest way to set up a guest account is to use the anonftp package, even if you do not want to provide anonymous FTP service. Just install the package temporarily for the purpose of creating a single guest account. Here are the steps needed to create a guest account:

### 1. Create the guest user account.
Become root and create the guest user account in the same manner that you create a real user account. This example assumes this guest user account is called mrfrog and that it was created using the usual useradd command, as follows:

```
useradd mrfrog
```

Set a desired password for mrfrog, using the following command:

```
passwd mrfrog
```

### 2. Stop Telnet access.
Change mrfrog's default shell to /bin/true, using the following command:

```
chsh mrfrog
```

When prompted for the new shell path, enter `/bin/true`. This disallows mrfrog from telnetting to the system, to ensure that mrfrog can't use telnet to access the server and browse other user or system files.

Edit the /etc/passwd file and append /./ to the existing home directory path. For example, if the /etc/passwd file has a line similar to the following:

```
mrfrog:$1$dev33vylewv.:516:519:/home/mrfrog:/bin/true
```

then change it to this:

```
mrfrog:$1$dev33vylewv.:516:519:/home/mrfrog/./:/bin/true
```

The ./ sequence is used to tell the FTP server to perform chroot operation on the /home/mrfrog directory.

Edit the /etc/shells file and add /bin/true at the end of the file. This makes the /bin/true program a valid shell option. Note that the /bin/true program does nothing and exits immediately after it is run. This makes it a good candidate for a shell that needs to be validated but denies the user anything and then exits. Because exit from the shell logs out the user, the user never gets a chance to do anything when a Telnet connection is attempted.

### 3. Install the anonftp package.
If you already have the anonftp package installed on your system, skip this step and go to Step 4. Otherwise, get the latest anonftp package and install it by running the rpm command:

```
rpm -ivh anonftp-2.6.1-1386.rpm
```

Your anonftp package name will vary based on your system architecture and anonftp version. Also, the anonftp package won't install if you don't already have an FTP server, such as wu-ftpd.

### 4. Copy the anonftp package files to the guest user's home directory.
Change the directory to ~ftp and use the following command to copy all the files and directories to ~mrfrog:

```
tar cvf - * | ( cd ~mrfrog ; tar xvf - )
```

All you really need are the ~ftp/bin, ~ftp/etc, and ~ftp/lib directories. You can delete the ~ftp/pub directory or any other directory that you might already have in your ~ftp directory.

### 5. Update the ~mrfrog/etc/passwd and ~mrfrog/etc/group files.
Edit the ~mrfrog/etc/passwd file and remove the line for the FTP user. Append the exact password line for mrfrog from the /etc/passwd file. However, remove mrfrog's password and replace it with a * to make it invalid. For example:

```
mrfrog:$1$dev33vylewv.:516:519::/home/mrfrog/./:/bin/true
```

This line needs to be copied to ~mrfrog/etc/passwd, and the password needs to be replaced such that the line looks like the following:

```
mrfrog:*:516:519::/home/mrfrog/./:/bin/true
```

Modify the ~/mrfrog/etc/group file and add the mrfrog line found in /etc/group. This assumes that you have not somehow disabled Red Hat's default feature for automatic creation of a private group by the same name as the new user. In other words, when you create a user by using the useradd program, it automatically creates a private group for that user with the same name. So, when you created mrfrog, you should have also automatically created a group called mrfrog in the /etc/group. If you have changed the default behavior of the useradd program or manually created the user, create a group for this user and add it to the ~/mrfrog/etc/group file. Also, remove the ftp group from the ~/ftp/etc/group file.

### 6. Set directory and file permissions.
Change the directory/file permissions as follows:

```
chown mrfrog.mrfrog ~/mrfrog
chmod 750 ~/mrfrog
```

The chown command sets the user and group ownership to mrfrog's user and group. The chmod command makes the ~/mrfrog directory accessible only to the mrfrog user and group.

```
chown -R root.root ~/mrfrog/etc ~/mrfrog/bin ~/mrfrog/lib
```

This command changes the ownership of the etc, bin, and lib subdirectories under ~/mrfrog to the root user and group.

```
cd ~/mrfrog
chmod -R 111 *
```

The first command changes the directory to ~/mrfrog, and the second command makes all the files and directories executable-only for everyone.

```
cd etc; chmod 444 *
```

These commands change the directory to the ~/mrfrog/etc directory and change the file permissions to read-only for everyone.

### 7. Set the guestgroup in /etc/ftpaccess.
Because you want the real user mrfrog to be a guest user, you need to add mrfrog's group (which is also called mrfrog) to the guestgroup group list. For example,

```
guestgroup mrfrog
```

allows any member of the mrfrog group (found in /etc/group) to be a guest user. In other words, the FTP server will perform the chroot operation. For the mrfrog user, the FTP server will chroot to /home/mrfrog.

### 8. Test the account.
FTP to the server and log in as mrfrog. If everything is set up correctly, you will see only the home directory of this user. Try to upload a file or create a directory. You should be allowed to do these operations. However, whether or not mrfrog is allowed to delete, overwrite, or rename files depends on what you have set for these operations in /etc/ftpaccess. For example, the default /etc/ftpaccess includes the following lines:

```
chmod  no  guest,anonymous
delete  no  guest,anonymous
overwrite  no  guest,anonymous
rename  no  guest,anonymous
```

These lines prohibit the guest accounts from performing chmod, delete, overwrite, or rename operations. If you want to allow these operations for guest accounts, remove "guest" from the default type-list in these lines and turn them into the following lines:

```
chmod  no  anonymous
delete  no  anonymous
overwrite  no  anonymous
rename  no  anonymous
```

If you don’t want to keep the anonftp package around or don’t want to have anonftp capabilities on your FTP server, either remove the package files from the appropriate (~ftp) directory or simply run the following:

```
rpm -e anonftp-2.6-1.i386.rpm
```

Don’t forget to use the appropriate filename, because your version or architecture might be different from what was just described.

## Creating virtual FTP sites
If you have multiple domains and need to support separate FTP servers (ftp.domain-1.com, ftp.domain-2.com, and so on), you can use virtual FTP service, which allows you to share a single-server system for
