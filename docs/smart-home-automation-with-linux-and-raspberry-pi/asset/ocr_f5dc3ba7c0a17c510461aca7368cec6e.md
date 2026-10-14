> **Note** Subversion stores its own work files inside the current directory, meaning they will each be littered with `.svn` folders. This is only a mild nuisance for end users but can cause bigger problems when they appear in system configuration folders such as `/etc`.

To make a direct copy of one set of files from one directory to another, you can probably use cp at the end of each day. However, this will wastefully copy files that haven’t changed, and so rsync was born. rsync is a very old copy and backup program but is still a venerable workhorse. I make backups of my code directory, for example, with this single line:

```
rsync -a code steve@remote-backup-host.com:~/backup/daily
```

I recover them (for testing⁸) with this:

```
rsync -a steve@remote-backup-host.com:~/backup/daily code
```

The options here perform a recursive update, while maintaining all symlinks, permissions, and user settings and is the most typical in home situations. The manual pages detail other possibilities.

rsync does have two problems, however. The first is that it's available primarily for Unix-oriented platforms. Versions are available for Windows (such as DeltaCopy and the version with Cygwin), but they take a little while to set up and can be tricky.

The second issue is that it requires a password to be interactively given in order to log in to the remote site. This is a nuisance and prevents any kind of automatic backup. For a remote site to allow a user to connect without a password, they must first establish an alternative form of trust—in this case, the exchange of public keys. To copy from machine A to machine B, B must have a copy of A’s public key. To copy from machine B to machine A, A must have a copy of B’s public key. In our case, machine A is at home with our files, while B is a remote machine for backup. So, our home machine must generate a key for the user who’ll be doing the copying.

```
ssh-keygen -t rsa
```

which by default can be found in `~/.ssh/id_rsa.pub`. This is then copied to the remote machine (perhaps using a password-directed rsync) and appended to the list of authorized keys that the remote user will accept:

```
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

Once this is done, you should be able to rsync without a password:

```
rsync -a --bwlimit=100 steve@remote-backup-host.com:~/backup/daily_code
```

Note that this limits the bandwidth (with the bwlimit argument) to 100 kilobytes per second so that other applications can make use of the Internet, since rsync and ssh are rather greedy when teamed up together.

One potential administration problem that can exist here is for the home user to be refused a connection because the address from which they’re connecting does not match the one used in the key. This can happen when the hostname is something simply like linuxbox1 but appears to the remote machine as netpc-london-isp.com or something equally unhelpful. The target machine, by comparison, will usually have a fixed name because it must be addressable from the outside world. Because the home machine may change (at the whim of the ISP), the easiest solution is to reverse all the instructions given here! That is, use the remote server to connect to the