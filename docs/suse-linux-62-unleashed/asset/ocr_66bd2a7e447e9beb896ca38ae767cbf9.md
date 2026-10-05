# Testing CD Images

Just as you can use mkfs to create a filesystem inside an ordinary file, you can mount filesystems contained in ordinary files by using the loop device driver described previously. The first example of mounting a loopback filesystem is a demonstration of how you can test a CD image.

# Other Character Devices

Several other details of character devices, such as /dev/null, are used frequently.

# The Controlling Terminal Device—/dev/tty

Most processes have a controlling terminal, particularly if they were started interactively by a user. The controlling terminal, which I refer to as simply /dev/tty, is used for initiating a conversation directly with the user (for example, to ask him something). One example can be with the crypt command:

```
$ fmt diary.txt | crypt | mail -s Diary confidant@linux.org
```

Enter key:
$

Here, the crypt command has opened /dev/tty to obtain a password. It was not able to use its own standard output to issue the prompt and its standard input to read the password because they are being used for the data to be encrypted.

> Note
The crypt command is not included with SuSE Linux (although you'll find a cryptdir utility). Of course, it's unusual to send email encrypted with crypt. A better choice is probably PGP, GnuPG, or specialized scripts and configuration files, such as ppg4pine (a PGP/GnuPG filter for the pine email program).

More useful examples are commands that need to ask the operator something even if the input and output are redirected. A case in point is the cpio command, which prompts the operator for the name of a new tape device when it runs out of space. See the “/dev/null and Friends” section later in this chapter for another example.