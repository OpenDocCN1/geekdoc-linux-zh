The shell you get depends on the option that is shown in the Linux password file, known as /etc/passwd. An example from this file for user mj is:

```
mj:x:501:501:michael jang:/home/mj:/bin/bash
```

The most common Linux shell is known as bash, which stands for the Bourne Again SHell. When you log in, bash starts to the requirements of its resource control file, known as .bashrc, which is located in your home directory. If you change your shell, you need to change the .profile file in your home directory and create a resource control file for your new shell. For example, if you wanted to use the shell known as ash, you'd need a resource control file named .ashrc.

> The dot in front of a file makes it hidden. You can list all files, hidden and otherwise, with the ls -a command.

# A Note on Passwords

When you look at your /etc/passwd file, you might think your passwords are well hidden. However, if a cracker finds this file, he/she can easily determine your password, especially if you use dictionary words.

The most secure way to create a password is based on a combination of letters and numbers. For example, popular password cracking programs might find a dictionary-based password like pepper in a matter of minutes. In contrast, it would probably take the same program weeks to crack a password like lz29tceW (which might stand for "I eat 29 fish tacos every Wednesday").

> In the Linux world, malicious users are known as crackers. Linux hackers are people who just want to make, or hack, better software. Crackers, on the other hand, try to crack into your passwords and software for destructive reasons.

# Logouts, Cache, and Shutdowns

If you just turn off your Linux computer, you can easily lose data that you thought you saved. For example, when you save data to a floppy drive, Linux may not write to the drive until you unmount it.

It turns out that most of your available memory (RAM + swap partition) is dedicated to programs and cache. As you open more programs, the information in the cache is "flushed" to make room for additional incoming data.