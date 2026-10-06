# CHAPTER 22 Secure Shell (SSH)

+   * **Port** Specifies the port number on which ssh listens. The default value is 22.

+   * **Protocol** Specifies the protocol versions ssh supports. The possible values are 1 and 2. Note that protocol version 1 is generally considered insecure now.

+   * **AllowTcpForwarding** Specifies whether Transmission Control Protocol (TCP) forwarding is permitted. The default is **yes**.

+   * **X11Forwarding** Specifies whether X11 forwarding is permitted. The argument must be **yes** or **no**. The default is **no**.

+   * **ListenAddress** Specifies the local address on which the SSH daemon listens. By default, OpenSSH listens on both Internet Protocol 4 (IPv4) and Internet Protocol version 6 (IPv6) sockets. If you need to specify a particular interface address, you can change this.

> NOTE sshd_config is a rather odd configuration file. Unlike other Linux configuration files, out-of-the-box comments (#) in the sshd_config file denote the default values of the options—that is, comments represent defaults that are already compiled in.

# # Using OpenSSH

OpenSSH comes with several programs that are covered in this section: the ssh client program, common the Secure Copy (scp) program, and the Secure FTP (sftp) program. The most common application you will probably use is the ssh client program.

# # Secure Shell (ssh) Client Program

With the ssh daemon started, you can use the ssh client program to log into a machine from a remote location in the same manner that you do Telnet. The key difference between ssh and Telnet, is that your SSH session is encrypted, and your Telnet session is not.

The ssh client program will usually assume that you need to log into the remote system (destination) as the same user with which you are logged into the local system (source). However, if you need to use a different login (instance, if you are logged in as root on one host and want to ssh to another and as the user **yang**), all you need to provide is the -l option along with the desired login. For example, if you need to log into the host server-B as the user yangang from server-A, you would type

```
root@server-A -]# ssh -l yangang server-B
```

Or you could use the username@host command format, like so:

```
root@server-A -]# ssh yangang@server-B
```

You would then be prompted with a password prompt from server-B for the user yangang’s password.