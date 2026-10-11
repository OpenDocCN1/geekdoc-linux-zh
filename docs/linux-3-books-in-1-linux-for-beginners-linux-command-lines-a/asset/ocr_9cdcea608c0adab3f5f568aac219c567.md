password to protect the updated settings.

# Restricting the Use of Old Passwords

You can ensure users do not use old passwords when they are prompted to update their passwords. Your Linux server will save the old passwords in the file /etc/security/opasswd. You can ensure your server does this using the PAM module. If you are unsure of how to do this, follow the steps given below:

+   1.  If you use CentOS, Fedora or RHEL, you can open the file `/etc/pam.d/system-auth`. To do this, run the command: `# vi /etc/pam.d/system-auth`

+   2.  If you use Ubuntu or Debian, you can open the file `/etc/pam.d/common-password` using the command `# vi /etc/pam.d/common-password`

+   3.  You need to add the following command to the auth section in your configuration file: `auth sufficient pam_unix.so likeauth nullok`

Once you do this, you need to add the following lines to the configuration file to ensure a user does not reuse his last few passwords. You can decide the number of passwords you want the server to store.

```
password    sufficient    pam_unix.so nullok use_authtok md5 shadow remember=5
```

This line will indicate to the server that it needs to remember the user's last five passwords. So, if the user enters one of the earlier passwords, he will receive an error from Linux asking him to choose a different password.

# Checking Listening Ports

You need to look at the different ports in your server and view them along with the services they provide. To do this, you can run the following command: `netstat -tunlp`. Based on the list you receive, you can determine if there are any ports you need to disable from the system. You can do this using the command `chkconfig`. You can then close all the ports in the server which you do not need. To do this, you can run the command: `chkconfig`