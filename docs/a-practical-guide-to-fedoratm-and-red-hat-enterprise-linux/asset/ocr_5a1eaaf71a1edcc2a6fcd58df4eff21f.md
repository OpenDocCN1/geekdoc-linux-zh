# OPENSsh Tools

The OpenSSH project provides a set of tools that replace **rcp**, **rsh**, and others with secure equivalents. These tools are installed by default in Fedora/RHEL and can be used as drop-in replacements for their insecure counterparts. The OpenSSH tool suite is covered in detail in Chapter 18.

# **LPI**  telnet: Logs In On a Remote System

You can use the TELNET protocol to interact with a remote computer. The **telnet** utility (**telnet** package), a user interface to this protocol, is older than **ssh** and is not secure. Nevertheless, it might work where **ssh** (page 693) is not available (there is more non-UNIX support for TELNET access than for **ssh** access). In addition, some legacy devices, such as terminal servers, facilities infrastructure, and network devices, still do not support **ssh**. The following example shows Sam using **telnet** to log in on a remote system that is running the **in.telnetd** daemon (**telnet-server** package):

```
[sam@guava ~]$ telnet plum
Trying 192.168.206.181...
Connected to plum.
Escape character is '^A'.
Fedora release 19 (Schrodinger's Cat)
Kernel 3.10.3-300.fc19.x86_64 on an x86_64 (2)
plum login: sam
Password:
Last login: Tue Mar  8 13:20:14 from 192.168.206.180
...
[sam@plum ~]$ logout
Connection closed by foreign host.
[sam@guava ~]$
```

# **telnet versus ssh**

When you connect to a remote UNIX or Linux system, **telnet** presents a textual login: prompt. Because **telnet** is designed to work with non-UNIX and non-Linux systems, it does not assume your remote username is the same as your local username (**ssh** does make this assumption). In some cases, **telnet** requires no login credentials.

# **security**  **telnet** is not secure

Whenever you enter sensitive information, such as your password, while you are using **telnet**, it is transmitted in cleartext and can be read by someone who is eavesdropping on the session.

In addition, **telnet** allows you to configure special parameters, such as how using RETURNS or interrupts are processed (**ssh** does not give you this option). When using **telnet** between UNIX and/or Linux systems, you rarely need to change any parameters.

When you do not specify the name of a remote host on the command line, **telnet** runs in an interactive mode. The following example is equivalent to the previous **telnet** example:

```
[sam@guava ~]$ telnet
telnet> open plum
Trying 192.168.206.181...
Connected to plum.
Escape character is '^A'.
...
```