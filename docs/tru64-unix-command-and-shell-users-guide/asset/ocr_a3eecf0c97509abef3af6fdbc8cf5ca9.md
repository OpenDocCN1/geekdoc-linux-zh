There are three cu local commands for tasks that are performed very often. You enter these commands from the remote host to perform tasks on the local host while you continue working on the remote host. These commands are preceded by a tilde and a percent symbol:

~%cd directory_name    Changes the directory on the local host
~%take from [to]       Copies a file from the remote host to the local host
~%put to [from]        Copies a file from the local host to the remote host

For example, while connected by cu to remote host moon, you can change the current directory on local host earth from /usr/geog/ocean to /usr/geog/ocean/pacific by entering the following command:

```
moon% ~%cd pacific
```

While connected by cu to remote host moon, you can copy the file, /usr/ETI/clavius to the file /usr/NASA/decode on local host earth by entering the ~%take local command at the remote system prompt:

```
moon% ~%take /usr/ETI/clavius /usr/NASA/decode
```

While connected by cu to remote host moon, you can copy the local file /usr/NASA/jupiter to the file /usr/ETI/clavius/hal9 on the remote host by entering the ~%put local command at the remote system prompt:

```
moon% ~%put /usr/NASA/jupiter /usr/ETI/clavius/hal9
```

# Note

Before using the ~%take and ~%put commands, verify that the destination directory exists. Unlike the uucp command, these cu local commands do not create intermediate directories during file transfers.

You can transfer only ASCII files with ~%take and ~%put. (For example, a PostScript file is an ASCII file, but an executable file is not.)

# 14.3.1.5 Using cu to Connect a Local Host to Several Remote Hosts

You can enter the cu command to connect host X to host Y, log on to host Y, and then enter the cu command there to connect to host Z. You then have one local host, X, and two remote hosts, Y and Z.

You can run an operating system command on host Z after you log in there. Then, from Z, you can run commands on the other hosts as follows:

+   - To run a command on host X, prefix the command with a single tilde (~)