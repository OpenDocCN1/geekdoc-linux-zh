
# PROBLEM 25

Symptom: Can't rsh to remote hosts.

Problem: You turned off rshd.

Fix: For now, you can do one of two things while you get used to rdist.

You can temporarily turn rsh back on by making the appropriate changes to /etc/inetd.conf (see Chapter 2), and adding this to your /etc/hosts.deny file:

```
in.rshd: ALL except servername
```

where servername is the machine on which you're running rdist. (Don't forget that you'll need a .rhosts or hosts.equiv on the remote host because .rhosts in particular can create a security hole.)

If, however, you can ssh to the remote host without a password (this requires matching host keys and authorized keys or hosts.equiv), just put the following code into a script called (for example) sish:

```
#!/bin/sh
ssh -q $0
```

Then (assuming sish is in the current directory), you can use rdist as follows:

```
$ rdist -P ./sish
```

(We'll get into more details on how to use ssh with rdist later.)

## Options

We've now introduced one of rdist's options, -P. rdist has two kinds of options: normal (regular) and dist options. Regular options are the same as in other programs: path names, configuration files, flags, and so on. Dist options control the remote distribution, and are specified with -o on the command line, as in this example:

```
$ rdist -oremove,younger,verify
```

This line tells rdist to remove files that are present on the remote host, but aren't in the local directory. It also instructs rdist to ignore files on the remote that have a newer modification time than those of the local copy, and to verify only (that is, to say what rdist needs to do) without actually doing it.

A dist option in a Distfile looks like this:

```
( www SRC ) -> ( mikado atlantic )
    install -oremove,younger ;
```

The second line is a command. In addition to specifying dist options, commands allow even tighter distribution control by comparing certain file parameters (such as the date). Here's more about commands.

## Commands

### except, except_pat

Ignore files and directories (don't update them). except pat takes regular expressions as arguments and ignores files or directories that match.

Examples:

```
except lib ;
except pat ^/usr/local/etc/.*\.conf$ ;
```

**PROBLEM 26**

**Symptom:** Some files mysteriously don't get updated.

**Problem:** Going overboard with except_pat.

**Fix:** Use the --verify dist option and examine the output. Try to start all expressions with a caret (^) and end them with a dollar sign ($). The regular expression in

```
except_pat etc/.*\.conf ;
```

matches files in /etc, /usr/etc, and /usr/local/etc (that is, if those directories are among those specified for the dist in the first place).

### install

Specify options or alternate installation directories. We've already seen dist options in examples such as

```
install -oremove,iglinks ;
```

For alternate installation directories, rdist behaves differently, depending on the source files. For the Distfile

```
( stuff ) -> ( atlantic pacific )
    install -oremove newstuff ;
```

the file or directory stuff is distributed as newstuff on the remote hosts. However, the following Distfile demonstrates a different scenario:

```
( morestuff/one morestuff/two morestuff/3/4 stuff ) -> ( atlantic pacific )
    install -oremove newstuff ;
```

In this case, rdist puts morestuff/one and morestuff/two into newstuff/one and newstuff/two on the remote hosts, but morestuff/3/4 becomes newstuff/4, and stuff goes into newstuff/stuff!

Why does rdist do this? It's trying to match items up, replacing as much of the base directory as possible. If rdist knows for certain that the source path name is a directory (in the case of morestuff and morestuff/3), it replaces all of the path name with the argument to install (here, with newstuff). But in our example, rdist doesn't know right away if stuff is a directory. If stuff is just a file, trying to put its contents into newstuff would be pointless

# PROBLEM 27

Symptom: rdist behaves differently with a single argument.

Problem: Design of rdist.

Fix: If your needs are fairly simple, use the whole dist option (described below) to force items to appear in the target directory without any path mangling. Try not to use the directory option to an rdist command with any complex arguments, because the resulting directory structure can be unpredictable. Split things up in the Distfile if you need to.

### notify

Send the results of the rdist to a user, for example:

```
notify foo@example.com ;
```

This option is really useful only if you want to notify different people of specific changes within the same Distfile. Otherwise, you can just log rdist's output to a file and mail it to the user(s).

### cmdspecial, special

When a certain file is distributed to a machine, special instructs rdist to run a program on that machine immediately. Here's an example for a syslogd and its configuration file:

```
special /etc/syslog.conf " /bin/kill -HUP `cat /var/run/syslogd.pid`"
```
