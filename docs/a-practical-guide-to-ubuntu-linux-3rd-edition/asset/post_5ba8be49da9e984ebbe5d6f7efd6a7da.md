
same security as ssh. The scp utility asks for a password when one is required. The format of an scp command is

```
scp [[user@]from-host:]source-file [user@]to-host:]destination-file]
```

where from-host is the name of the system you are copying files from and to-host is the system you are copying to. The from-host and to-host arguments can be local system names, FQDNs (page 1149) of systems on the Internet, or IP addresses. When you do not specify a host, scp assumes the local system. The user on either system defaults to the user on the local system who is giving the command; you can specify a different user with user@.

The source-file is the file you are copying, and the destination-file is the resulting copy. Make sure you have read permission for the file you are copying and write permission for the directory you are copying it into. You can specify plain or directory files as relative or absolute pathnames. (A relative pathname is relative to the specified or implicit user’s home directory.) When the source-file is a directory, you must use the -r option to copy its contents. When the destination-file is a directory, each of the source files maintains its simple filename. When the destination-file is missing, scp assumes the user’s home directory.

Suppose Sam has an alternate username, sls, on plum. In the following example, Sam uses scp to copy memo.txt from the home directory of his sls account on plum to the allmemos directory in the working directory on the local system. If allmemos was not the name of a directory, memo.txt would be copied to a file named allmemos in the working directory.

```
sam@dog:~$ scp sls@plum:memo.txt allmemos
sls@plum’s password: 
memo.txt 100% 4084kB 4.0MB/s 00:01
```

As the transfer progresses, the percentage and number of bytes transferred increase and the time remaining decreases.

In the next example, Sam, while working from peach, copies the same file as in the previous example to the directory named old in his home directory on speedy. For this example to work, Sam must be able to use ssh to log in on speedy from plum without using a password. For more information refer to “Authorized Keys: Automatic Login” on page 677.

```
sam@peach:~$ scp sls@plum:memo.txt speedy:old
sam@plum’s password:
```

# OPTIONS

This section describes some of the options you can use with scp.

- -C (compression) Enables compression.
- -o option (option) Specifies option in the format used in configuration files (discussed shortly).
- -p port Connects to port port on the remote host. This option is given in uppercase for scp and in lowercase for ssh.
- -p (preserve) Preserves the modification and access times as well as the modes of the original file.
- -q (quiet) Does not display the progress information as scp copies a file.
- -r (recursive) Recursively copies a directory hierarchy.
- -v (verbose) Displays debugging messages about the connection and transfer. Useful if things are not going as expected.

# SFTP: A SECURE FTP CLIENT

As part of OpenSSH, Ubuntu Linux provides sftp, a secure alternative to ftp (page 687). Functionally the same as ftp, sftp maps ftp commands to OpenSSH commands. You can replace ftp with sftp when you are logging in on a server that is running the OpenSSH daemon, sshd. Once you are connected to a system with sftp, give the command ? to display a list of commands. For secure communication, use sftp or scp to perform all file transfers requiring authentication. Refer to the sftp man page for more information.

Ubuntu also offers lftp, which is more sophisticated than sftp and supports sftp. The lftp utility provides a shell-like command syntax that has many features, including support for tab completion and the ability to run jobs in the background. Use /etc/lftp.conf to configure lftp and see the lftp man page for more information.

# ~/.SSH/CONFIG AND /ETC/SSH/SSH_CONFIG CONFIGURATION FILES

It is rarely necessary to modify OpenSSH client configuration files. For a given user there may be two configuration files: ~/.ssh/config (user) and /etc/ssh/ssh_config (global). These files are read in this order and, for a given parameter, the first one found is the one that is used. A user can override a global parameter setting by setting the same parameter in her user configuration file. Parameters given on the ssh or scp command line take precedence over parameters set in either of these files.

A user’s ~/.ssh/config file must be owned by the user (the owner of the ~ / directory) and must not be writable by anyone except the owner; if it is, the client will exit with an error message. This file is typically set to mode 600 as there is no reason for anyone except its owner to be able to read it.

Lines in the configuration files contain declarations. Each of these declarations starts with a keyword that is not case sensitive, followed by whitespace, followed by case-sensitive arguments. You can use the Host keyword to cause declarations to apply to a specific system. A Host declaration applies to all the lines between it and the next Host declaration.

- CheckHostIP yes | no
  Identifies a remote system using the IP address in addition to a hostname from the known_hosts file when set to yes (default). Set it to no to use a hostname only. Setting CheckHostIP to yes can improve system security.

- ForwardX11 yes | no
  When set to yes, automatically forwards X11 connections over a secure channel in non- trusted mode but does not set the DISPLAY shell variable. If ForwardX11Trusted is also set to yes, the connections are made in trusted mode. Alternatively, you can use -X on the command line to redirect X11 connections in untrusted mode. The default value for this parameter is no; set it to yes to enable X11 forwarding. For X11 forwarding to work, you must also set X11Forwarding to yes in the /etc/sshd_config file on the server (page 680). For more information refer to “Forwarding X11” on page 681.

- ForwardX11Trusted yes | no
  Works in conjunction with ForwardX11, which must be set to yes for this declaration to have any effect. When this declaration is set to yes (as it is on Ubuntu Linux systems) and ForwardX11 is set to yes, this declaration sets the DISPLAY shell variable and gives remote X11 clients full access to the original (server) X11 display. Alternatively, you can use -Y on the command line to redirect X11 connections in trusted mode. The default value for this declaration is no but Ubuntu Linux sets it to yes. For X11 forwarding to work, X11Forwarding must also be set to yes in the /etc/sshd_config file on the server (page 680). For more information refer to “Forwarding X11” on page 681.

- HashKnownHosts
  Causes OpenSSH to hash hostnames and addresses in the ~/.ssh/known_hosts file when set to yes. The hostnames and addresses are written in cleartext when it is set to no. Ubuntu Linux sets this declaration to yes to improve system security. See page 668 for more information on the known_hosts file.

- Host hostnames
  Specifies that the following declarations, until the next Host declaration, apply only to hosts that hostnames matches. The hostnames can include ? and * wildcards. A single * specifies all hosts. Without this keyword, all declarations apply to all hosts.

- HostbasedAuthentication yes | no
  Tries rhosts authentication when set to yes. For a more secure system, set to no (default).

- HostKeyAlgorithms algorithms
  The algorithms is a comma-separated list of algorithms the client uses in order of preference. Choose algorithms from ssh-rsa or ssh-dss. The default is ssh-rsa,ssh-dss.

- Port num
  Causes OpenSSH to connect to the remote system on port num. The default is 22.

- StrictHostKeyChecking yes | no | ask
  Determines whether and how OpenSSH adds host keys to a user’s known_hosts file. Set this option to ask to ask whether to add a host key when connecting to a new system, set it to no to add a host key automatically, and set it to yes to require that host keys be added manually. The yes and ask arguments cause OpenSSH to refuse to connect to a system whose host key has changed. For a more secure system, set this option to yes or ask. The default is ask.

- TCPKeepAlive yes | no
  Periodically checks whether a connection is alive when set to yes (default). Checking causes the ssh or scp connection to be dropped when the server crashes or the
