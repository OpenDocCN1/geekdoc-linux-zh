untrusted X11 forwarding set up failed or No xauth data. These warnings are not critical when forwarding X over SSH, and should not worry you.

# Remote X Commands with OpenSSH

Logging into another machine just to run an X program—or any program—can be an annoyance. The -f option to ssh lets you run a command on another machine while keeping the SSH session itself backgrounded. This looks like you’re executing a command directly on the other host. Give the command right after the host you want to access. For example, if I want to run an xterm on wrath I could run:

```
$ ssh -f wrath xterm
```

The client will connect to the server and display whatever login text the server shows. The SSH client then goes into the background, restoring your command prompt on your local system even as it runs the command on the remote system.

Note that remote commands are run in the user’s full logon environment. Any files attached to the user’s shell, such as .cshrc or .profile, are sourced. This might give you trouble, depending on the application you’re running.

Backgrounding forwarded X-over-SSH sessions is very useful, but forwarding TCP ports over SSH is even more useful. We’ll look at that next.