To use SSH for remote access, you type the SSH client's name followed by the server name. SSH passes your current username to the server, which attempts to use the same username to authenticate you. If you want to use a different username on the server than on your current system, you should include the `-1 username` parameter on the command line or prepend the username to the hostname with an at-sign (@), as follows:

```
```
$ ssh ecernan@apoll o.luna.edu
ecernan@apollo.luna.edu's password:
Last login: Tue Sep 30 10:43:37 from gemini.luna.edu
[ecernan@apoll o ecernan]$ 
```
```

![](bbox=[0.15, 0.32, 0.27, 0.39])

The first time you make a connection to a given server, you may see a message informing you that the authenticity of the server can't be verified. The message goes on to display a code associated with the server. If you want to continue connecting, type `yes` in response to the query.

You may omit the username and at-sign if your username is the same on both systems. Once you've logged in with SSH, you can use the system much as you would from the console—by typing text-mode commands, editing files with text-mode editors, and so on. Because SSH encrypts all data, it's extremely unlikely that your original password, or the password you type when you use su, will be usable to anybody who intercepts the data stream.

A variant on using SSH for remote login access is to use the protocol for running a specific program. Simply type the command you want to run at the end of the `ssh` command line, as in `ssh apollo.luna.edu cat /etc/fstab` to view the contents of `/etc/fstab` on apollo.luna.edu.

SSH does further duty as a secure file transfer protocol. On the client side, you can use the `scp` or `sftp` commands to handle this job. The `scp` command is similar to `cp`, but it operates across an SSH link. You add the hostname and, optionally, remote username to either the source or destination filename, as follows:

```
```
$ scp gemini.txt gene@apollo.luna.edu:
...or...
$ scp gene@apollo.luna.edu:xxii.txt ./
```
```

The first command copies the local file `gemini.txt` to the home directory of the user `gene` on apollo.luna.edu. The second copies copies `xxii.txt` from apollo.luna.edu to the local computer. If your username on both systems is the same, you may omit the username and at-sign (@) from the command.