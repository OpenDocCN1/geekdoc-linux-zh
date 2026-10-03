# rsh

You use the rsh (remote shell) command to execute a shell on another system on the network. The other system must trust your ID on the current system. The following example uses rsh to get a long listing of the directory /etc on systemB:

```
rsh systemB ls -la /etc
```

# rexec

The rexec command is also used to execute a shell on a remote system. This command differs from rsh in that you must enter a password. At many sites, rsh is disabled for security reasons, and rexec is used as a replacement.

# rwho

The rwho command produces output similar to the who command, which was described in Chapter 9, but for all systems on the network.

# finger

The finger command displays information about users logged on to the local system or other systems. If finger is used without an argument, it gives information concerning users currently logged in. If finger is used with an argument (for example, the username glenda), it displays information about all users matching the argument. You can also use the finger command to look up users on a remote system by specifying the user as username@host. To protect user privacy, many remote systems do not allow remote fingering of their systems.