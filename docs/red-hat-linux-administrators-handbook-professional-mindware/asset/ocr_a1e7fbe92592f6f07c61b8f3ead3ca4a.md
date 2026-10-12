7. Set the guestgroup in /etc/ftpassess. Because you want the real user mrfrog to be a guest user, you need to add mrfrog’s group (which is also called mrfrog) to the guestgroup group list. For example,

```
guestgroup  mrfrog
```

allows any member of the mrfrog group (found in /etc/group) to be a guest user. In other words, the FTP server will perform the chroot operation. For the mrfrog user, the FTP server will chroot to /home/mrfrog.

8. Test the account. FTP to the server and log in as mrfrog. If everything is set up correctly, you will see only the home directory of this user. Try to upload a file or create a directory. You should be allowed to do these operations. However, whether or not mrfrog is allowed to delete, overwrite, or rename files depends on what you have set for these operations in /etc/ftpassess. For example, the default /etc/ftpassess includes the following lines:

```
chmod
    no    guest,anonymous
delete
    no    guest,anonymous
overwrite   no    guest,anonymous
rename
    no    guest,anonymous
```

These lines prohibit the guest accounts from performing chmod, delete, overwrite, or rename operations. If you want to allow these operations for guest accounts, remove guest from the default type-list in these lines and turn them into the following lines:

```
chmod
    no    anonymous
delete
    no    anonymous
overwrite   no    anonymous
rename
    no    anonymous
```

If you don’t want to keep the anonftp package around or don’t want to have anonftp capabilities on your FTP server, either remove the package files from the appropriate (-ftp) directory or simply run the following:

```
rpm -e  anonftp-3.0-6.i386.rpm
```