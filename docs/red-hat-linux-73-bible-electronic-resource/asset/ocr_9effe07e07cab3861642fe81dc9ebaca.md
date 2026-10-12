This shows that the `sshd` service is set to run in system states 3, 4, and 5 (normal bootup states) and set to be off in all other states. You can turn on the SSH service, if it is off, for your default run state, by typing the following as root user:

```
# chkconfig --level 345 sshd on
```

This line turns on the SSH service when you enter run levels 3, 4, or 5. To start the service immediately, type the following:

```
# /etc/init.d/sshd start
```

# Using the ssh, sftp, and scp commands

Three commands you can use with the SSH service are `ssh`, `sftp`, and `scp`. Remote users use the `ssh` command to login to your system securely. The `scp` command lets remote users copy files to and from a system. The `sftp` command provides a safe way to access FTP sites.

Like the normal remote shell services, secure shell looks in the `/etc/hosts.equiv` file and in a user’s `.rhost` file to determine whether it should allow a connection. It also looks in the ssh-specific files `/etc/shosts.equiv` and `.shosts`. Using the `shosts.equiv` and the `.shosts` files is preferable because it avoids granting access to the nonencrypted remote shell services. The `/etc/shosts.equiv` and `.shosts` files are functionally equivalent to the traditional `hosts.equiv` and `.rhosts`, so the same instructions and rules apply.

Now you are ready to test the SSH service. From another computer on which SSH has been installed (or even from the same computer if another is not available), type the `ssh` command followed by a space and the name of the system you are connecting to. For example, to connect to the system `ratbert.glaci.com`, type:

```
# ssh ratbert.glaci.com
```

If this is the first time you have ever logged in to that system using `ssh`, it will ask you to confirm that you really want to connect. Type `yes` and press `Enter` when it asks this:

```
Host key not found from the list of known hosts.
Are you sure you want to continue connecting (yes/no)?
```

It should then prompt you for a user name and password in the normal way. The connection will then function like a normal `telnet` connection. The only difference is that the information is encrypted as it travels over the network. You should now also be able to use the `ssh` command to run remote commands.

The `scp` command is similar to the `rcp` command for copying files to and from Linux systems. Here is an example of using the `scp` command to copy a file called `memo` from the home directory of the user named `jake` to the `/tmp` directory on a computer called `maple`:

```
$ scp /home/jake/memo maple:/tmp
password: *******
memo    100%  ***************   153     0:00
```