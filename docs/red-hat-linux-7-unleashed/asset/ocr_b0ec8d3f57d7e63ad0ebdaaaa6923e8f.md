# Other Character Devices

Several other varieties of character devices, such as `/dev/null`, are used frequently.

# The Controlling Terminal Device—`/dev/tty`

Most processes have a controlling terminal, particularly if they were started interactively by a user. *The controlling terminal*, which I refer to as simply `/dev/tty`, is used for initiating a conversation directly with the user (for example, to ask him something). An example is the `crypt` command:

```
$ fmt diary.txt | crypt | mail -s Diary confidant@linux.org
Enter key:
$
```

Here, the `crypt` command has opened `/dev/tty` to obtain a password. It was not able to use its own standard output to issue the prompt and its standard input to read the password because they are being used for the data to be encrypted.

> **Note**
> 
> Of course, it's unusual to send email encrypted with `crypt`. A better choice is probably **GnuPG**. This is an Open Source replacement for PGP.

More useful examples are commands that need to ask the operator something even if the input and output are redirected. A case in point is the `cpio` command, which prompts the operator for the name of a new tape device when it runs out of space. See the section “`/dev/null` and Friends” later in this chapter for another example.

# Nonserial Mice

Many computers have bus or PS/2 mice instead of serial mice. This arrangement has the advantage of keeping both of the two standard serial ports free, but the disadvantage of using up another IRQ. These devices are used by `gpm` and the X Window System, but most other programs don’t interact with them directly. Setting up your system with these mice is easy; the Red Hat Linux installation process pretty much takes care of it for you. If you have problems with your mouse, however, you should read the manual page for `gpm` and the Linux BusMouse HOWTO.