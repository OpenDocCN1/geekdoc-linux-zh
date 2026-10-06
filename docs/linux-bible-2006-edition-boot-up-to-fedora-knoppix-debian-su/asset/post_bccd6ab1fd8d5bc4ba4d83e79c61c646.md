
## 208 Part II Running the Show

The lines begin with a # character [which are] comments. Other lines contain two columns of information. The left field is a semicolon-separated list (spaces won't work) of message type and message priorities. The right field is the log file to which messages should be sent.

To send the messages to another computer (the loghost) instead of a file, start by replacing the log filename with the @ character followed by the name of the loghost. For example, redirect the output normally sent to the messages, secure, and maillog files, make these changes to the preceding file:

```
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*:info:mail:news:authpriv.none:cron.none @loghost

# The authpriv file has restricted access.
authpriv.* @loghost

# Log all the mail messages in one place.
mail.* @loghost
```

The messages will now be sent to the syslog running on the computer named loghost. The loghost was not an arbitrary choice. It is customary to create such a host name and make an alias to the actual system acting as the loghost. That way, if you ever need to switch the log duties to a different machine, you need to change only the loghost alias: you do not need to reprint the syslog.conf file on every computer.

On the log side, that must run syslog so you will need to listen on the network by -r option to log messages from other machines. In Fedora systems, adding a -r option to the SYSLOG_OPTIONS variable in /etc/sysconfig/syslog file and restarting the syslog service (service syslog restart). It must also have UDP port 514 accessible to be used by syslog (check the /etc/services file), so you might need to add a firewall rule to that.

## Understanding the messages Log File

Because of the many programs and services that record information to the messages log file, it is important that you understand the format of this file. You can get a good early warning of problems developing on your system by examining this file. Each line in the file is a single message recorded by some program or service. Here is a snippet of an messages log file:

```
Feb 25 11:04:32 test network: Binding up loopback interface: succeeded
Feb 25 11:04:35 test network: Binding up interface eth0: succeeded
Feb 25 13:01:14 test network: vsftpd(pam_unix)[10565]: authentication failure;
logname= uid=0 eid=0 tty= rhost=10.0.0.5 user=chris
Feb 25 14:44:24 toys(pam_unix)[11439]: session opened for
user by chris(uid=500)
```

This is really very simple when you know what to look for. Each message is divided into five main parts. From left to right, they are:

- The date and time that the message was logged
- The name of the computer from which the message came
- The program or service name to which the message pertains
- The process number (enclosed in square brackets) of the program sending the message
- The actual text message

Take another look at the preceding snippet. In the first two lines, you can see that the network was restarted. The next line shows that the user named chris tried and failed to get the FTP server on this system from a computer at address 10.0.0.5 (he typed the wrong password and authentication failed). The last line shows su to become root user.

By occasionally reviewing the messages secure files, it's possible to catch a cracking attempt before it is successful. If you see an excessive number of connection attempts for a particular service, especially if they are coming from systems on the Internet, you may be under

## Using Secure Shell Tools

The Secure Shell (ssh) tools are a set of client and server applications that allow you to do basic communications (remote login, remote copy, remote execution, and so on) between computers and your Linux system. Because communication is encrypted between the (typically the ssh daemon process) and clients (such as ssh, scp, and sftp), these tools are inherently more secure than similar, older UNIX tools such as rsh, rcp, and login.

Most Linux systems include the ssh server. If you use the Fedora or Red Hat Enterprise Linux distributions, for example, the following client and server software packages include the ssh software: openssh, openssh-clients, and openssh-server packages.

### Starting the ssh Service

Linux systems that come with the ssh service already installed are configured for it to start automatically. In Fedora and RHEL systems, the ssh daemon is started from the /etc/init.d/ssh startup script. To make sure the service is set up to start automatically in Fedora, RHEL, and other RPM-based Linux systems, using the following (as root user):

```
# chkconfig --list ssh
sshd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

This shows that the ssh service is set to run in system states 2, 3, 4, and 5 (normal bootstrap states) and set to be off in all other states. You can turn on the SSH service, if it is off, or for your default state, by typing the following as root user:

```
# chkconfig sshd on
```

This line turns on the ssh service when you enter run levels 2, 3, 4, or 5. To start the ssh service immediately, by typing the following:

```
# service sshd start
```

Other Linux distributions may simply start the sshd daemon from entry in the /etc/rc.d directory from rc.sshd. In any case, you can find out the sshd daemon is currently running by typing your system the following:

```
$ ps ax | grep sshd
Ss 00:00 /usr/sbin/sshd
```

The preceding example shows that the sshd daemon is running. If that is the case, and your firewall allows secure shell service (TCP port 22), you should be able to use ssh commands to access your system. (Any other configuration you want to restrict what the sshd daemon will allow is typically done in the /etc/ssh/sshd_config.file)

## Using the ssh, sftp, and scp Commands

Three commands can be used with the SSH service: ssh, sftp, and scp. Remote users use the ssh command to log in to your system or remotely execute a command on your system. The scp command provides a safe way to access FTP files and through the ssh service (for sites that offer access to their FTP content).

Like the normal remote shell, secure shell looks in the /etc/hosts.equiv file in a user's .host file to determine whether it should allow a connection. It also looks in system-specific files /etc/hosts.equiv and .hosts. Using the hosts.equiv and the .hosts files is preferable because it avoids granting access to the encrypted remote shell. The /etc/hosts.equiv and .hosts files are functionally equivalent to the traditional hosts and .hosts files, so the same instructions and rules apply.

Now you are ready to test the ssh service. From another computer on which ssh has been installed (even from the same computer if another is not available), type the ssh command followed by a space and the name of the system you are connecting to. For example, to connect to the system ratbert.glaci.com, type:

```
# ssh ratbert.glaci.com
```

If this is the first time you have logged in to this system using the ssh command, the system will ask you to confirm that you really want to connect. Type yes and press Enter when it asks this:

The authenticity of host 'ratbert.glaci.com (199.170.17.18)' can't be established.
RSA fingerprint is xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx.
Are sure you want to continue connecting (yes/no)?

It should prompt you for username and password. The connection will then function like a normal login (in other words, you can begin commands). The only difference is that the information is encrypted as it travels over the network. You now also be able to use the ssh command to run commands from a shell.

The scp command is similar to the rcp command for copying files to from Linux systems. Here is an example of using the scp command to copy a file called memo from the home directory of the user jake to the /tmp directory on a computer:

```
$ scp /home/jake/memo memo:/tmp
jake@maple's password: *********
memo 100% |************| 153 0:00
```

Enter the password for username (if a password is requested). If the password is accepted, the remote system indicates that the file has been copied successfully.

Similarly, the sftp command starts an interactive FTP session with an FTP server that supports SSH connections. Many security-conscious people use sftp to other clients because it provides a secure connection between you and the remote host. Here's an example:

```
$ sftp.handsonhistory.com
Connecting to ftp.handsonhistory.com
jake@ftp.handsonhistory.com's password: ***********
sftp>
```

At this point you can begin an interactive FTP session. You can use get and put commands as files as you would using an FTP client, but with the comfort of knowing that you are working on a secure connection.

The sftp command, as with ssh and scp, requires the service to be running on the server. If you can't connect to a FTP server using sftp, the SSH service may not be available.
