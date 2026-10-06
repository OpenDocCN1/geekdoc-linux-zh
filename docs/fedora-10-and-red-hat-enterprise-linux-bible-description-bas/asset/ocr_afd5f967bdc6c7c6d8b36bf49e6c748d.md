# Chapter 14: Computer Security Issues 603

This line turns on the SSH service when you enter levels 2, 3, 4, or 5. To start the service immediately, type the following:

```
# /etc/init.d/sshd start
```

> TIP: If you aren't able to connect to the ssh service from another computer, check that the firewall is open on your server to allow access to tcp port 22. That's the default port on which ssh listens for requests.

# Using the ssh, sftp, and scp commands

Three commands you can use with the ssh service are ssh, sftp, scp. Remote users use the ssh command to log in your secure system. The scp command lets users copy files to and from a system. The sftp command provides a safe way to access FTP sites.

Like the normal remote shell services, secure shell looks in the /etc/hosts.equiv file and in a user .hosts file to determine whether it should allow a connection. It also looks in the ssh-specific files /etc/hosts.equiv and .shosts. Using the hosts.equiv and the .shosts files is avoids granting access to the nonencrypted remote shell services. The /etc/shosts.equiv and .shosts files are functionally equivalent to the traditional hosts.equiv and .hosts files, the same instructions and rules apply. Type man hosts.equiv for further information.

Now you are ready to start the SSH service. From another computer on SSH has been installed (or from the same computer if another is not available), type the ssh command followed by a space and the name of the system you are connecting to. For example, to connect to the system ratbert.glaci.com, type:

```
$ ssh ratbert.glaci.com
```

If this is the first time you have logged into that system using the ssh command, it will ask you to confirm that you want to connect. Type yes and press Enter when it asks this:

```
The authenticity of host 'ratbert.glaci.com' (199.170.177.18) can't be established.
RSA key fingerprint is xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx.
Are you sure you want to continue connecting (yes/no) yes
```

> CAUTION: If you use an auth request a second time, this could possibly be a man-in-the-middle attack.

If you don't specify a user name when you start the ssh connection, the ssh daemon allows you to use the user name you are logged in as from the client. If you want to log in as a different user name (such as chris, for example), you could type the following:

```
$ ssh chris@ratbert.glaci.com
```

or

```
$ ssh -l chris ratbert.glaci.com
```