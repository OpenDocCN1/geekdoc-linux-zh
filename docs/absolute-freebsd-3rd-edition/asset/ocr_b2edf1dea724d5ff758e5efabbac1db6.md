# Setting and Viewing File Flags

Set flags with chflags(1). For example, to be sure that nothing replaces a server’s kernel, you could do this:

```
`# chflags schg /boot/kernel/kernel`
```

You’d need to remove this flag to perform system updates.

You can recursively change the flags on an entire directory tree with the -R flag. For example, to make all of /bin directory immutable, run this command:

```
`# chflags -R schg /bin`
```

And boom! Your basic system binaries can’t be changed.

To see what flags are set on a file, use ls -lo.

```
`# ls -lo log
-rw-r--r---   1 mrlucas mrlucas   sappnd  0 Nov 12 12:37 log`
```

The sappnd entry tells us that the system append-only flag is set on this log. For comparison, if a file has no flags set, it looks like this:

```
`# ls -lo log
-rw-r--r---   1 mrlucas mrlucas   - 0 Nov 12 12:37 log`
```

The hyphen in place of the flag name tells us that no flag has been set.

An out-of-the-box FreeBSD install doesn’t have many files marked with flags, but you can flag anything you want. On one system that I fully expected to be hacked, I went berserk with chflags -R schg in various system directories to prevent anyone from replacing system binaries with trojaned versions. It might not stop an attacker from getting in, but imagining their frustration improved my mood.

To remove a file flag, use chflags and a n in front of the flag name. For example, to unset the schg flag on your kernel, enter this command:

```
`# chflags noschg /boot/kernel/kernel`
```