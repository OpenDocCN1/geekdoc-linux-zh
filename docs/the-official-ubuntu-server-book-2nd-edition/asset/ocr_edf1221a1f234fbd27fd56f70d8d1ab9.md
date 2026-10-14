characters to match, but in this case, since there is only one character in it, it acts just as if I were grepping for bash. Of course, since the grep command itself has brackets in it, it doesn't show up in the result.

# Shortcut to a Command Path

There are times when you want to look at a shell script you have in your binary path but you can't quite remember whether it's in /bin, /sbin, /usr/bin, /usr/local/bin, or somewhere else. While you could just keep hitting the tab key until you find it, the which command will search through your path and output the full path to the command you list:

```
$ which vim
/usr/bin/vim
```

If I wanted to run ls -l against the vim binary but I wasn't sure what directory it was in, I could just type

```
$ ls -l `which vim`
1rwxrwxrwx 1 root root 21 2008-03-21 22:22 /usr/bin/vim ->
/etc/alternatives/vim
```

When you surround a command with backticks (`), it will run the command and the output will appear in its place. I especially like to do this when I want to edit a custom shell script I've written and don't know where I saved it.

# Wipe a Drive in One Line

Be careful with this command! As a sysadmin you often have systems you need to get rid of and need to erase the hard drives so no private company data gets out. A simple way to do this is to use the dd command to read from the special /dev/zero device and output to the drive you want to erase. When the command is done, the entire drive will be all zeros. So if I wanted to completely erase /dev/sdb, I would type

```
$ sudo dd if=/dev/zero of=/dev/sdb
```