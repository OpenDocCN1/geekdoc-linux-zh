
## Checking for setuid permission

Another popular setting called set user ID (or setuid for short) can be a security hazard. When the setuid permission is enabled, the file executes under the user ID of the file’s owner. In other words, if an executable program is owned by root and the setuid permission is set, no matter who executes that program, it runs as if root is executing it. This permission means that the program can do a lot more (for example, read all files, create new files, and delete files) than what a normal user program can do. Another risk is that if a setuid program file has some security hole, crackers can do a lot more damage through such programs than through other vulnerabilities.

You can find all setuid programs with a simple find command (remember to type `su -` to become root):

```
find / -type f -perm +4000 -print
```

You see a list of files such as the following:

```
/bin/su
/bin/ping
/bin/eject
/bin/mount
... lines deleted ...
```

Many of the programs have the setuid permission because they need it, but check the complete list and make sure that there are no strange setuid programs (for example, setuid programs in a user’s home directory).

If you want to see how these permissions are listed by the ls command, type `ls -l /usr/bin/passwd` and you see the permission settings:

```
-rwsr-xr-x 1 root shadow 74952 Aug 29 14:52 /usr/bin/passwd
```

The s in the owner’s permission setting (rws) tells you that the setuid permission is set.

## Securing the Network

To secure your SUSE Linux system, you have to pay attention to both host security and network security. The distinction between the two types of security is somewhat arbitrary because securing the network involves fixing up things on the host that relate to what Internet services your system offers. In this section, I explain how you can secure the Internet services (mostly by not offering unnecessary services), how you can use a firewall to stop unwanted network packets from reaching your network, and how to use Secure Shell for secure remote logins.

### Securing Internet services

For an Internet-connected Linux system (or even one on a LAN that’s not connected to the Internet), a significant threat is the possibility that someone could use one of many Internet services to gain access to your system. Each service — such as mail, Web, or FTP — requires running a server program that responds to client requests arriving over the TCP/IP network. Some of these server programs have weaknesses that can allow an outsider to log in to your system — maybe with root privileges. Luckily, Linux comes with some facilities that you can use to make the Internet services more secure.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_319_0.png)

Potential intruders can employ a *port-scanning tool* — a program that attempts to establish a TCP/IP connection at a port and to look for a response — to check which Internet servers are running on your system. Then, to gain access to your system, the intruders can potentially exploit any known weaknesses of one or more services.

### Turning off stand-alone services

To provide Internet services such as Web, mail, and FTP, your Linux system has to run server programs that listen to incoming TCP/IP network requests. Some of these servers are started when your system boots, and they run all the time. Such servers are called *stand-alone* servers. The Web server and mail server are examples of stand-alone servers.

Another server, called xinetd, starts other servers that are configured to work under xinetd. Some servers can be configured to run stand-alone or under a superserver such as xinetd. For example, the vsftpd FTP server can be configured to run stand-alone or to run under the control of xinetd.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_319_1.png)

You can turn the servers on or off by using the chkconfig command. For example, to turn off the FTP service, type `chkconfig vsftpd off`.

### Configuring the Internet superserver

In addition to stand-alone servers such as a Web server or mail server, there is another server — xinetd — that you have to configure separately. The xinetd server is called *Internet superserver* because it can start other servers on demand.

The xinetd server reads a configuration file named `/etc/xinetd.conf` at startup. This file, in turn, refers to configuration files stored in the `/etc/xinetd.d` directory. The configuration files in `/etc/xinetd.d` tell xinetd which ports to listen to and which server to start for each port. Type `ls /etc/xinetd.d` to see a list of the files in the `/etc/xinetd.d` directory on your system. Each file represents a service that xinetd can start. To turn off any of these services, type `chkconfig filename off` where *filename* is the name of the configuration file in the `/etc/xinetd.d` directory. After you turn any of these services on or off, you must restart the xinetd server; otherwise, the changes don’t take effect. To restart the xinetd server, type `/etc/init.d/xinetd restart`. This command stops the xinetd server and then starts it again. When it restarts, it reads the configuration files, and the changes take effect.

### Configuring TCP wrapper security

A security feature of xinetd is its use of a feature called *TCP wrapper* to start various services. The *TCP wrapper* is a block of code that provides an access-control facility for Internet services, acting like a protective package for your server. The TCP wrapper can start other services, such as FTP and vnc (a server that enables other computers to view and interact with your computer’s graphical desktop); but before starting a service, it consults the `/etc/hosts.allow` file to see whether the host requesting service is allowed that service. If nothing appears in `/etc/hosts.allow` about that host, the TCP wrapper checks the `/etc/hosts.deny` file to see if it denies the service. If both files are empty, the TCP wrapper provides access to the requested service.

Here are the steps to follow to tighten the access to the services that `inetd` or `xinetd` are configured to start:

1. **Use a text editor to edit the `/etc/hosts.deny` file, adding the following line into that file:**

```
ALL:ALL
```

This setting denies all hosts access to any Internet services on your system.

2. **Edit the `/etc/hosts.allow` file and add to it the names of hosts that can access services on your system.**

For example, to enable only hosts from the 192.168.1.0 network and the `localhost` (IP address 127.0.0.1) to access the services on your system, place the following line in the `/etc/hosts.allow` file:

```
ALL: 192.168.1.0/255.255.255.0 127.0.0.1
```

3. If you want to permit access to a specific Internet service to a specific remote host, you can do so by using the following syntax for a line in `/etc/hosts.allow`:

```
server_program_name: hosts
```

Here `server_program_name` is the name of the server program, and `hosts` is a comma-separated list of hosts that can access the service. You may also write `hosts` as a network address or an entire domain name, such as `.mycompany.com`.

### Using Secure Shell (SSH) for remote logins

SUSE Linux comes with the *Open Secure Shell* (OpenSSH) software that uses public-key cryptography to authenticate users and to encrypt the communication between two hosts, so users can securely log in from remote systems and copy files securely.

In this section, I briefly describe how to use the OpenSSH software in SUSE Linux. The OpenSSH software is installed during SUSE Linux installation. OpenSSH uses public-key encryption where the sender and receiver both have a pair of keys — a public key and a private key. The public keys are freely distributed, and each party knows the other’s public key. The sender encrypts data by using the recipient’s public key. Only the recipient’s private key can then decrypt the data.

To use OpenSSH, you first need to start the `sshd` server and then generate the host keys. Here’s how:

1. If you want to support SSH-based remote logins on a host, start the `sshd` server on your system. Type `ps ax | grep sshd` to see if the server is already running. If not, in a terminal window type `su -` to become root, and turn on the SSH service.
2. Type `/etc/init.d/sshd start` to start the `sshd` server immediately. To ensure that the server starts the next time you reboot the system, type `chkconfig sshd on`.
3. Generate the host keys with the following command:

```
ssh-keygen -d -f /etc/ssh/ssh_host_key -N ''
```

The `-d` flag causes the `ssh-keygen` program to generate DSA keys, which the SSH2 protocol uses. If you see a message saying that the file `/etc/ssh/ssh_host_key` already exists, that means that the key pairs were generated during SUSE Linux installation. In that case, press `n` to avoid overwriting the keys and continue to use the existing file.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_321_0.png)
