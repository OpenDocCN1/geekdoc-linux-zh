# # Users and Ownership

File owners are set up by the system during installation. Linux system files are owned by IDs such as root, uucp, and bin. Do not change the ownership of these files, even if you are logged in as root. That’s because the permissions are set correctly when Linux installs the software, and if you change them, you may prevent the system from accessing the file properly.

![](bbox=[0.03, 0.3, 0.78, 0.44])

> Although it’s sometimes tempting to change ownerships of system files, this can cause real problems for utilities that don’t run as root and need to read those files. In most cases if you change the ownership or the permissions of a system file, the utilities that use that file will lock up or terminate. Change ownership of files only when you know they are user files!

You can use the chown (change ownership) command to change the ownership of a file. The syntax of the chown command is

```
chown <owner> <filename>.
```

owner indicates where to insert the user ID that will own the file, and filename indicates the name of the file that you are setting ownership for. You can use wildcards with the chown command to indicate a number of files at once.

In the following example, you change the ownership of the myfile to the login bill:

```
darkstar:~$ ls -l myfile
-rw-r--r-- 1 fido users 114 Dec 7 14:31 myfile
darkstar:~$ chown bill myfile
darkstar:~$ ls -l myfile
-rw-r--r-- 1 bill users 114 Dec 7 14:31 myfile
```

Before you can change the login of the file owner, Linux checks to confirm that it exists. After you have changed the ownership of the file, you may not be able to do anything else with the file, so be careful. To make any further changes to the file myfile or to chown it back to fido, you must use either su or log in as bill and use the chown command to set you back to the owner.