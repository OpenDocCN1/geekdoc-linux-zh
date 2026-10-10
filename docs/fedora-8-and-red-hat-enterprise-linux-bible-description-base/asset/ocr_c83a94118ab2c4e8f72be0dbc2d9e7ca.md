How does the system check your password in this case? When you log in, the system encodes the password you entered, compares the resulting scrambled string with the scrambled string that is stored in the password file, and grants you access only if the two match. Have you ever asked a system administrator what the password on your account was once to be told that the system administrator doesn't know? If so, this is why: The administrator really doesn't have the password, only the encrypted version. The non-encoded password exists only at the moment you type it.

# ## Breaking encrypted passwords

There is a problem with people being able to see encrypted passwords, however. Although it may be difficult (or even impossible) to reverse the encryption of a trapdoor algorithm, it is very easy to encode a large number of password guesses and compare them to the encoded passwords in the password file. This is, in order of magnitude, more efficient than trying actual login attempts for each user name and password. If a cracker can get a copy of your password file, the cracker has a much better chance of breaking into your system.

Fortunately, Linux and all modern UNIX systems support a shadow password file by default. The shadow file is a special version of the `passwd` file that only root can read. It contains the encrypted password information, so passwords can be left out of the `passwd` file, which any user on the system can read. Linux supports the older, single password file method as well as the newer shadow password file. You should always use the shadow password file (it is used by default).

# ## Checking for the shadow password file

The password file is named `passwd` and can be found in the `/etc` directory. The shadow password file is named `shadow` and is also located in `/etc`. If your `/etc/shadow` file is missing, then it is likely that your Linux system is storing the password information in the `/etc/passwd` file instead. Verify this by displaying the file with the `less` command.

```
# less /etc/passwd
```

Something similar to the following should be displayed:

```
root:DkS6GUke799fQ:0:0:root:/root:/bin/bash
bin:*:1:1:bin:/bin
daemon:*:2:2:daemon:/sbin:
.
.
.
mary:KpRUo2ZzmYSTA:500:100:Mary Smith:/home/mary:/bin/sh
joe:OsXRzvKnaKasi:501:100:Joe Johnson:/home/joe:/bin/sh
jane:pTNoueYbjvX.:502:100:Jane Anderson:/home/jane:/bin/sh
bob:Ju2vY7A0X6KZw:503:100:Bob Renolds:/home/bob:/bin/sh
```