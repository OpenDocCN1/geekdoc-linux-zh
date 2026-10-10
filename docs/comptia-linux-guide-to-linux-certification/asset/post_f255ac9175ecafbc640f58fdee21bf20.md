
## Secure Shell (SSH)

Although the telnet command can be quickly used to perform remote administration, it doesn't encrypt the information that passes between computers. Secure Shell (SSH) was designed as a secure replacement for telnet (and other legacy commands, such as rsh, rlogin, and rcp) that encrypts information that passes across the network. As a result, the SSH daemon (sshd) is installed by default on nearly all Linux distributions.

![](img/c27875544958897d817484d558c208c8_584_0.png)

To connect to a remote Linux computer running sshd, you can use the ssh command followed by the host name or IP address of the target computer. For example, you can connect to a computer with the host name of appserver using the ssh appserver command. Your local user name will be passed to the server automatically during the SSH request, and you will be prompted to supply the password for the same user on the target computer. If you need to log in using a different user name on the remote appserver computer, you can instead use the ssh -l username appserver command or the ssh username@appserver command. A sample ssh session is shown in the following output:

```
[root@server1 ~]# ssh root@appserver
root@appserver's password:
Last login: Thu Sep 2 14:29:06 2015 from 10.0.1.3
[root@server1 ~]# who
          root    :0          Aug 10 14:13
          root    pts/8       Aug 10 14:14 (:0.0)
          root    pts/9       Aug 10 14:14 (10.0.1.3)
[root@server1 ~]# exit
Connection to appserver closed.
[root@server1 ~]#
```

You can also use the PuTTY program on a Windows computer to connect to sshd running on a Linux, UNIX, or Macintosh computer.

![](img/c27875544958897d817484d558c208c8_584_1.png)

When you connect to a new computer for the first time using SSH, you will be prompted to accept the RSA encryption fingerprint for the target computer, which is stored in ~/.ssh/known_hosts for subsequent connections. If the target computer's encryption keys are regenerated, you will need to remove the old key from the ~/.ssh/known_hosts file before you connect again.

![](img/c27875544958897d817484d558c208c8_584_2.png)

SSH can also be used to transfer files between computers. For example, to transfer the `/root/sample` file on a remote computer called `appserver` to the `/var` directory on the local computer, you could run the following command:

```
[root@server1 ~]# ssh root@appserver cat /root/sample > /var/sample
root@appserver's password:
[root@server1 ~]#
```

Alternatively, to transfer the `/root/sample` file on the local computer to the `/var` directory on a remote computer called `appserver`, you could run the following command:

```
[root@server1 ~]# ssh root@appserver cat < /root/sample ">" /var/sample
root@appserver's password:
[root@server1 ~]#
```

Although SSH is used to perform command-line administration of remote systems, the `-X` option to the `ssh` command can be used to tunnel X Windows information through the SSH connection if you are using the `ssh` command within a GUI environment. For example, if you start a command-line terminal within a GNOME desktop and run the command `ssh -X root@appserver`, you will receive a command prompt where you can type commands as you would in any command-line SSH session. However, if you type a graphical command (e.g., `gnome-control-center`), you will execute the graphical utility on `appserver` across the SSH tunnel. All graphics, keystrokes, and mouse movement will be passed between X Windows on `appserver` and X Windows on the local system.

Since SSH is typically used to perform remote administration, `sshd` is usually configured to allow root logins and a wide range of encryption algorithms by default. However, you can configure the functionality of `ssh` by editing the `/etc/ssh/ssh_config` file. Most of this file is commented and should only be edited to change the default settings that `sshd` uses when servicing SSH clients. The most commonly changed options in this file are those that deal with authentication and encryption. By default, `sshd` uses a secure challenge-response authentication method that ensures that the password is not transmitted on the network, but this can be changed to Kerberos authentication.

![](img/c27875544958897d817484d558c208c8_585_0.png)

> On Ubuntu Server 14.04, root access via SSH is denied by default. To enable it, you can modify the value of `PermitRootLogin` to `yes` within the `/etc/ssh/ssh_config` file.

Organizations use many types of encryption to secure communication on the network. Each type of encryption differs in its method of encryption and the cryptography key length used to encrypt data; the longer the key length, the more difficult it is for malicious users to decode the data. The main types of encryption supported by `sshd` are as follows:

- Triple Data Encryption Standard (3DES), which encrypts blocks of data in three stages using a 168-bit key length
- Advanced Encryption Standard (AES), an improvement on 3DES encryption and is available in 128-, 192-, and 256-bit key lengths
- Blowfish, an encryption algorithm that is much faster than 3DES and can use keys up to 448 bits in length
- Carlisle Adams Stafford Tavares (CAST), a general-purpose encryption similar to 3DES that is commonly available using a 128-bit key length
- ARCfour, a fast encryption algorithm that operates on streams of data instead of blocks of data and uses variable-length keys up to 2048 bits in length

In addition, all of the aforementioned types of encryption except ARCfour typically use Cipher Block Chaining (CBC), which can be used to encrypt larger amounts of data.

Client computers can use a /etc/ssh/ssh_config or ~/.ssh/ssh_config file to set SSH options for use with the ssh command, including the encryption types that can be used. However, the encryption types on the client computer must match those supported by the SSH server for a connection to be successful.

## Virtual Network Computing (VNC)

Like the -X option of ssh, Virtual Network Computer (VNC) is another graphical option for administering a Linux system remotely. After you install a VNC server daemon on a computer, other computers that run a VNC client can connect to the VNC server daemon across a network to obtain a desktop environment. VNC uses a special platform-independent protocol called Remote FrameBuffer (RFB) to transfer graphics, mouse movements, and keystrokes across the network.

![](img/c27875544958897d817484d558c208c8_586_0.png)

Since X Windows is not installed on Ubuntu Server 14.04 by default, we'll focus on the configuration of VNC on Fedora 20 in this section. However, the steps are similar on other Linux distributions.

On Fedora 20, you can install a VNC server by running the yum install tigervnc-server command. Next, you must configure the VNC Server by creating a VNC server configuration file that listens on a certain display number. To create a VNC server configuration file that listens on the third X Windows display, you can use the following command to copy it from the /lib/systemd/system/vncserver@.service template:

```
[root@localhost ~]# cp /lib/systemd/system/vncserver@.service /lib/systemd/system/vncserver@3.service
[root@localhost ~]#
```

![](img/c27875544958897d817484d558c208c8_586_1.png)

The port number to which the VNC server listens is 5900 plus the display number. The VNC server listed in the preceding output would be listed on port 5903.

![](img/c27875544958897d817484d558c208c8_586_2.png)

Next, you must edit the VNC server configuration file and, at minimum, modify the line(s) that indicate(s) the user who can connect (replace <USER> with a valid username). It's also good form to set the window geometry that is used when the session is started. For example, to grant user1 the ability to obtain a VNC window with dimensions 1024x768, you could edit the following line within /lib/systemd/system/vncserver@3.service to indicate the login name of user1 and geometry of 1024x768:

```
ExecStart=/sbin/runuser -1 user1 -c "/usr/bin/vncserver %i -geometry 1024x768"
```

Following this, you can execute the systemctl daemon-reload command to force all running daemons to re-read their configuration files, log in as user1, and run the vncpasswd command to set the VNC password that will be used for the VNC connection. The VNC password is stored in the ~/.vnc/passwd file; for user1, the VNC password will be stored in the /home/user1/.vnc/passwd file.

Finally, you can log back in as the root user, start the VNC server instance for the display number, and configure it to start automatically at system initialization using the following commands:

```
[root@localhost ~]# systemctl enable vncserver@3.service
[root@localhost ~]# systemctl start vncserver@3.service
[root@localhost ~]#
```

Next, other computers can connect to the VNC server using a VNC viewer program, such as RealVNC. When using a VNC viewer program to connect to a remote VNC server, you can specify the server name or IP address, port, and display number using the syntax server:port:display. For example, to connect to the VNC server that uses display number 2 on the computer server1.class.com, you could use the syntax server1.class.com:5902:2. You will then obtain a desktop session on the remote computer, as shown in Figure 12-9.

![](img/c27875544958897d817484d558c208c8_587_0.png)
