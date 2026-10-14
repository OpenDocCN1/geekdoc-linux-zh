
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

### Note

Before using the ~%take and ~%put commands, verify that the destination directory exists. Unlike the uucp command, these cu local commands do not create intermediate directories during file transfers.

You can transfer only ASCII files with ~%take and ~%put. (For example, a PostScript file is an ASCII file, but an executable file is not.)

## 14.3.1.5 Using cu to Connect a Local Host to Several Remote Hosts

You can enter the cu command to connect host X to host Y, log on to host Y, and then enter the cu command there to connect to host Z. You then have one local host, X, and two remote hosts, Y and Z.

You can run an operating system command on host Z after you log in there. Then, from Z, you can run commands on the other hosts as follows:

- To run a command on host X, prefix the command with a single tilde (~)
- To run a command on host Y, prefix the command with two tildes (~~)

Table 14-2 summarizes the most common cu local commands. For information about other cu local commands, refer to cu(1).

### Table 14-2: Local cu Commands

| Command | Description |
|---|---|
| ~. | Logs you off the remote host and terminates the remote connection. When connected to the remote host over a telephone line using a modem, this command does not always work. In such cases, press Ctrl/D to log off; then type a tilde and a period (~.) at the prompt and press the Return key to terminate the remote connection. |
| ~! | Returns the session from the remote host to the local host. Type a tilde and an exclamation point (~!) at the prompt and enter any command. To return to the remote host, press Ctrl/D. After establishing the cu connection, you can go back and forth between the two hosts by typing ~! (to go from remote to local) and pressing Ctrl/D (to go from local to remote). |
| ~$cd directory_name | Changes the current directory on the local host to that specified by the directory_name variable. If no directory name is specified, cu changes it to your home directory. |
| ~$take source[dest] | Copies a file from the remote to the local host. If you do not specify a dest destination file on the local host, the ~$take command copies the remote file to the local host and assigns the same file name. |
| ~$put source[dest] | Copies a file from the local to the remote host. If you do not specify a dest destination file on the remote host, the ~$put command copies the local file to the remote host and assigns the same file name. |
| ~$cmd | Executes the cmd command on the local host and sends the output to the remote host for execution by the remote shell. |

## 14.3.2 Using tip to Connect to a Remote Host

The tip command and its options enable you to connect to a remote host, log in to it, and perform tasks there from your local host. You can do tasks on each by switching back and forth between the two. If both hosts use the operating system, you can enter commands on the remote host from your local host.
