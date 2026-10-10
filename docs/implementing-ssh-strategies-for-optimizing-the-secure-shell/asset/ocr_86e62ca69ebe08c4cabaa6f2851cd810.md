This overview will allow you to understand the general uses of SFTP and also allow your decision-making process to be as informed as possible, depending on your business and security requirements for SFTP.

# SFTP with the OpenSSH SFTP Server

The OpenSSH SFTP subsystem is a great solution when requiring the secure transfer of file and folders from one machine to the next. As stated earlier, the use of the SFTP subsystem is enabled by default on the OpenSSH server; no special or additional steps are required. To ensure that the SFTP subsystem has been enabled, open the sshd_config file on the SSH server and scroll all the way to the bottom of the file. The SFTP subsystem information should be at the very end. Enter the following command to view the SFTP subsystem information in OpenSSH’s configuration file:

```
#cd /etc/ssh/ 
#more sshd_config
```

The following syntax should be at the end of the sshd_config file:

```
# override default of no subsystems
Subsystem	sftp	/usr/libexec/openssh/sftp-server
```

If the SFTP is not desired and only the use of the SSH service (shell or port forwarding access) is desired, the SFTP subsystem can be easily disabled by commenting out the “Subsystem SFTP” line. For example, in order to disable the SFTP subsystem in OpenSSH, make sure the last two lines of your sshd_config file look like the following:

```
# override default of no subsystems
# Subsystem sftp			/usr/libexec/openssh/sftp-server
```

Since you want to use the SFTP subsystem, make sure it is enabled (uncommented) in your /etc/ssh/sshd_config file. Now that you understand how to enable/disable the SFTP subsystem, examine the different ways you can use it with OpenSSH.

# Using OpenSSH for Management Purposes

First, I will discuss OpenSSH in terms of management purposes. Using any SFTP client, such as the command-line version that comes with OpenSSH (sftp), you can make a connection to a SFTP server to download files in a secure fashion. For example, if you want to copy the file called Commodore-Vic20.txt from the SFTP server, which has an IP address of 172.16.11.17, enter the following commands with your OpenSSH SFTP client: