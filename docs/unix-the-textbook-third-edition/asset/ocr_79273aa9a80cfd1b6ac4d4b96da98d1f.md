The following session shows remote login to a UNIX host that is not on your local network. Here, cs00.syi.pcc.edu is the FQDN of a host on the Internet, and the user is msarwar. Of course, cs00 must enter the valid password for msarwar to be able to log in. You could have used the rlogin -l msarwar@cs00.syi.pcc.edu command to establish this session.

```
$ rlogin cs00.syi.pcc.edu -l msarwar
msarwar's Password: xxxxxx
Last login: Wed Nov 22 06:41:41 2003 on /dev/pts/2 from upibm7.
egr.up.edu
[YOU HAVE NEW MAIL]
$ whoami
msarwar
$ hostname
cs00
$
```

In the following in-chapter exercises, you will use the rlogin and telnet commands to understand how they can be used to log on to a remote host on your network or on the Internet.

# EXERCISE 11.16

Use the telnet and rlogin commands to establish remote login sessions on a host on your LAN. Note that you will not be able to establish these sessions if the remote system does not run the corresponding server processes (e.g., telnetd or in.telnetd; use the ps -el command to determine this).

# EXERCISE 11.17

Try to establish a telnet session with the host locis.loc.gov and browse through the library at your pace.

# EXERCISE 11.18

Repeat all of the sessions shown in this section on telnet on your system. Do your results match ours?

# 11.8.7 Remote Command Execution

You can use the rsh (remote shell) command to execute a command on a remote host on your local network. Remote login is a relatively time-consuming process, but the rsh command gives you a faster way to execute commands on remote machines if the purpose of your remote login is to execute only a few commands. We used this command in Chapter 9 to illustrate the power of I/O redirection in UNIX; now we discuss it formally. The following is a brief description of the command.