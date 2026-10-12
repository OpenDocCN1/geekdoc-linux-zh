![](bbox=[0.1, 0.1, 0.62, 0.4])

# FIGURE 17.1

An xterm window

showing the pine

interface.

With the source code comes the latest POP3 and IMAP daemons. If you wish to create a POP3 or IMAP server on your Linux machine, pine provides the binaries to do so. After compiling the source to your specifications with working code, locate the imapd/ directory within the pine tree structure (no pun intended) and copy theipop2d,ipop3d, and imapd binaries to a directory within your path. Make sure that your /etc/services file includes them and then add them to your /etc/inetd.conf file. Once you have used HUP to hang up your inetd daemon, you can test to make sure that these daemons are also running by logging in to their respective ports. The POP3 daemon runs under port 110, whereas imapd runs under port 143. Test these ports much as you would sendmail.

```
telnet localhost 110
```

or

```
telnet localhost 143
```

You should also verify that these ports are visible from the outside world by testing them from a separate server.

Once you have made certain that pine is configured correctly, you can set up individual mail accounts that users can log in to from their home machines and download their mail onto their home machines.