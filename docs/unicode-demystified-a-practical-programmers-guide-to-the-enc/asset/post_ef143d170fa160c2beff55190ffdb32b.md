
# ssh: Logs in or Runs a Command on a Remote Computer

You can use the secure ssh utility to log in a remote system over the network. You might choose to use to a remote system to access a special-purpose application, use a device that is available only on that system, or because you know that the remote system is faster or not as busy as your local computer. While traveling, many people use ssh on a laptop to log in on a system at headquarters. From a GUI you are able to use many systems simultaneously by logging in each one, using a different terminal emulator window.

You can log in on a remote machine that is running the sshd daemon and that you have an account on. For information on configuring ssh, see page 102. All communication under ssh, including your name and password, is encrypted. Your login name is the same on the local and remote machines, the command ssh hostname, where hostname is the name of the machine that you want to log in on:

```
[bravo]$ ssh kudos
alex@kudos's password:
Last login: Sat Sep 14 06:51:59 from bravo
Have a lot of fun...
You have new mail.
[kudos]$
...
[kudos]$ logout
Connection to kudos closed.
[bravo]$
```

After you supply your password, you are running a shell on the remote machine. When you log out, the connection is broken, and you resume using your local computer. To log in with a user name different from the one you are using on the local machine, give the command ssh user@hostname, where user is your login name on the remote machine named hostname:¹⁶

```
[bravo]$ ssh watson@kudos
watson@kudos's password:
:
[kudos]$
```

The ssh utility also allows you to run a command on a remote system without logging in on that system. When you need to run more than one command, it is usually easier to log in and run the commands on the remote machine. The next example runs ls on the memos directory on the remote system kudos. The example assumes that the user running the command has a login on kudos and that memos is in the user's home directory on kudos:

```
[bravo] $ ssh kudos ls memos
alex@kudos's password:
memo.0921
memo.draft
[bravo]$
```

Suppose that if a file named memo.new is on your local machine and that you cannot remember whether it contains certain changes or whether you made these changes to the file named memo.draft on the system named kudos. You could copy memo.draft to your local system and run diff (page 67) on the two files, but then you would have similar copies of the file read across two systems. If you are not careful about removing the old copies when you are done, you may be confused again in a few days. Instead of copying the file, you can use ssh:

```
[bravo]$ ssh cat memos/memo.draft | diff memos.new -
```

When you run ssh, standard output of the command run on the remote machine is sent to the local shell as though the command had been run in place on the local machine. Unless you quote characters that have special meaning to the shell, they are interpreted by the local machine. In the preceding example output of the cat command on kudos is sent through a pipe on bravo to diff (running bravo), which compares the local file memos.new to standard input (-). The following command line has the same effect as diff run on the remote system:

```
[bravo]$ cat memos.new | ssh kudos diff - memos/memo.draft
```

Standard output from diff on the remote system is sent to the local shell, which displays it on the screen (because it is not redirected). Refer to page 1321 in Part III for more information on ssh.

# Optional

The ssh utility can tunnel other protocols. You can secure protocols including POP, X, IMAP, and WWW using ssh as a virtual private network (VPN) between the two systems. Assume that you have a POP client on your local machine, the POP server is on a remote network that is protected by a firewall, and that you can access the remote network using only ssh. You can tunnel the POP protocol, which uses port 110, through an ssh tunnel. In this example, kudos is the firewall gateway machine, pophost is the POP server, and 1550 is a local port that you selected to use on your end of the tunnel.

```
ssh -N -L 1550:pophost:110 kudos
```

# Chapter 9 Networking and the Internet

–N option allows ssh not to execute remote commands: ssh works only as a private network to forward ports. You can forward ports in either direction and in combination using the -L and -R flags. See the ssh man page for details.

Once you are authenticated, you can set your POP client so that the POP server is localhost and the POP port is 1550. Then, when the client fetches e-mail, it makes a connection to port 1500 on the local machine which is forwarded through the ssh tunnel to kudos and then to pophost port 110 where the real daemon is.

# scp: Copies a file/to a Remote Computer

The scp (secure copy) utility copies a file from one computer to another on a network. Using ssh to transfer files, scp uses the same authentication mechanism as ssh and therefore provides the same security. The scp utility asks for a password when it is needed for security. The format of an scp command is

```
scp [fromhost:source-file][tosthost:destination-file]
```

You can copy from or to your local machine between remote machines. When you specify a simple, or relative, filename, it is assumed to be relative to your home directory on machine. In the following example, Alex uses scp to copy rain.jpg from his working directory on bravo (which happens to be his home directory) to his home directory on kudos:

```
alex@bravo]$ scp rain.jpg kudos:
alex@kudos's password:
rain.jpg
100% |********************|3016 00:00
```

As the transfer progresses, the percent and number of bytes transferred and the time remaining decreases. The asterisks provide a visual representation of the transfer. Use the -r option to copy a directory. See the scp man page for more information.

# telnet: Logs in on a Remote Computer

You can use the TELNET protocol to interact with a remote computer. The telnet utility, a user interface to this protocol, is older than ssh and is not secure but may work where ssh is not available (there is more non-UNIX than there is for ssh). In addition, many legacy devices, such as terminal servers and network devices, do not support ssh.

```
[bravo]$ telnet kudos
Trying 130.128.52.2...
Connected to kudos.tcorp.com
Escape character is '^'
```

When you connect to a remote UNIX or GNU/Linux system through telnet, we are presented with a regular login: prompt. Unless you specify differently, telnet while ssh utility allows that your login name on the remote system matches the local system. Because telnet is designed to work with non-UNIX/Linux systems, it makes such assumptions.

```
kudos login: watson
Password:
Welcome to SuSE Linux 7.3 (i386) - Kernel 2.4.10-4GB (2).
You have old mail in /var/mail/watson.
Last login: Mon Feb 25 14:46:55 from bravo.tcorp.com
watson@kudos:~>

```
watson@kudos:~ logout
Connection closed by foreign host.
[bravo]$
```

# telnet Is Not Secure

> Whenever you expose sensitive information, such as your password, when you use telnet, it is transmitted in cleartext and can be read by someone who is listening in the session.

Another difference between these two utilities is telnet allows you to config many special characters, as how returns or interrupts are processed. When using telnet between two UNIX/Linux systems, you rarely need to change any parameters. When you do not specify the name of a remote host on the command line, telnet runs in an interactive mode. The following example is equivalent to the previous telnet example:

```
[bravo]$ telnet
telnet> open kudos
Trying 130.128.52.2...
Connected to kudos.tcorp.com
Escape character is '^'
```
