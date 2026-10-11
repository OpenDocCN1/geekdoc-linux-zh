This script should be set to executable with this command:

```
chmod +x sv
```

To run it, either place it in the path or prefix it with ./. The syntax to start a service is

```
sv samba start
```

# kill and killall

Controlling daemons can also include using the kill and killall commands, which work on the PID and command name, respectively.

kill and killall use the same signals; other than using PIDs and names, they are functionally similar. The kill command is fairly simplistic:

```
ps aux | grep smb
```

This returns the output shown here:

```
root 388 0.0 0.9 7324 2460 ? S 00:38 /usr/sbin/smbd -D
```

You then take the number from the second column and supply it as the argument to the kill command:

```
kill 388
```

If the program doesn't respond, or it is the parent process of a zombied process, use an *absolute kill* or the kill command with a -9 option to send the SIGKILL signal, such as

```
kill -9 388
```

The killall command works similarly. You can name the runaway or undesired processes by the actual command that is running, which is the last column of the ps output.

To kill all running instances of the Mozilla browser on your machine, as root you enter

```
killall mozilla-bin
```

If, for some reason, the browser doesn't respond, use the kill command with the -9 option to send a SIGKILL or absolute kill, like so:

```
killall -9 mozilla-bin
```

This forcibly removes the processes from memory; without even allowing them time to clean up memory and disk processes. So, be aware that using the kill and killall commands to abruptly terminate processes can leave