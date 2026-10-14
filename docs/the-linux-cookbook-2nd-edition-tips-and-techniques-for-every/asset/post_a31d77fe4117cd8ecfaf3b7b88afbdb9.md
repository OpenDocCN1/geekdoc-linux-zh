
This command is a toggle—type prompt again to turn file prompting back on for your session.

## 34.2.2 Downloading a File from a Remote Host

The get command works like put, but in reverse—specify a file on the remote system, and get saves a copy to the current directory on the local system. Again, use binary first when downloading non-text files. (You can also download text files with i, so it is good practice to always use it before you transfer files; most Linux systems are configured to set the type to i immediately upon connection).

⇒ To download the file `INDEX.gz` in the current directory on the remote system, saving it to your `/tmp` directory, type:

```
ftp> lcd ~/tmp [RET]
Local directory now /home/james/tmp
ftp> get INDEX.gz [RET]
local: INDEX.gz remote: INDEX.gz
Transferred 10942677 bytes
ftp>
```

**NOTES:** The mget command works like get but allows wildcards; as with mput, you will be prompted to verify each file unless you use the `prompt` command first to turn this off.

## 34.3 Using Secure Internet Services

```
OpenSSH
  DEB: ssh
  RPM: openssh
  WWW: http://www.openssh.com/
```

These newer methods involving secure, encrypted connections replace the older methods in the recipes described previously for connecting to a remote system and for transferring files to and from a remote system. Use them in place of `telnet` and `ftp` when enhanced security is desired, or required.

You can still use the old ways, and they may be fine for local networks, but on the Internet the secure variants have become the standard in most places—the Net is not the safe haven it was a decade ago, and in practice, few sites allow telnet access anymore.

The following recipes describe how to use the openssh implementation of the famous ssh ("Secure Shell") protocol. OpenSSH includes the contemporary replacements for older rlogin, rsh, and rcp secure-connection tools.

NOTES: The first time you use one of these tools to connect with a remote system, you may get a message telling you that the "host key" was not found in the list of known hosts, and asking whether or not to continue with the connection—answer "yes."

### 34.3.1 Making a Secure Shell Connection to a Remote Host

Use ssh to connect securely to a remote system. It opens a login connection on a remote system whose hostname you give as an argument.

⇒ To open a secure connection to arctic.example.org, type:

```
$ ssh arctic.example.org [RET]
ernie@arctic.example.org's password: snowshoe [RET]
Last login: Wed Aug 13 11:39:29 EDT 2003

Welcome to arctic.example.org!

[ernie@arctic ~]
```

In this example, the username ernie made a SSH connection to the system arctic.example.org, on which his password is "snowshoe." The "~ $" is the shell prompt on that system, where he can run commands until he exits by either running the exit command or by typing CTRL-D at a shell prompt.

If your username on the remote system differs from your username on your local system, use the -l option to specify a different username.

⇒ To open a secure connection to arctic.example.org with a remote user-name of scout, type:

```
$ ssh -l scout arctic.example.org [RET]
scout@arctic.example.org's password: igloo [RET]
Last login: Wed Aug 13 13:14:53 EDT 2003

Welcome to arctic.example.org!

You have new mail.
[scout@arctic ~]
```

In this example, the user logged into arctic.example.org with a user-name on that system of scout, whose password was "igloo."

### 34.3.2 Making a Secure File Copy to a Remote Host

Use scp to make secure file copies between your local system and a remote host. It takes as arguments the name of the file to copy from and the name of the file to copy to. For the file on the local system, just give the file name as usual; specify the file name on the remote system in this format:

```
user@remote:filename
```

For user, give the name of your username on the remote system (if it's the same as the local system, omit both it and the trailing at sign (@). For remote, give the hostname of the remote system to connect to, and for filename give the name of the file as it should appear in the home directory of user.

⇒ To copy the file index.html from your local_html directory to the public_html directory in your account on the system arctic.example.org, type (all on one line):

```
$ scp local_html/index.html arctic.example.org:public_html/index.html [RET]
ernie@arctic.example.org's password: snowshoe [RET]
index.html 100% |********************************| 2365 00:00
$
```

In this example, the user has a username of ernie on both systems; the progress of the copy is displayed on the screen before scp exits.

Use the -r option to copy an entire directory tree.
