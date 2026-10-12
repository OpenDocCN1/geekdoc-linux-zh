
Services on your Red Hat Linux system produce messages of different levels. Message levels, from most critical to least critical, are listed in Table 14-7.

### Table 14-7: Message Levels

| Level | What it Means |
| :--- | :--- |
| alert | immediate action needed |
| crit | Critical |
| debug | detailed processing information |
| emerg | system unusable |
| err | error condition |
| info | purely informational |
| notice | important, but not an error |
| warning | potential error |

The line shown in the example indicates that all messages from the info level (*.info) and above are logged to the /var/log/messages file. However, messages of types mail, news, authpriv, and cron are excluded because they are sent to other log files. All authpriv (authpriv.*) messages are logged to the /var/log/secure file. mail messages (mail.*) are all logged to the /var/log/maillog file.

With this default configuration of syslog, LogSentry should catch all major security related activities. There are a few situations, however, where you may want to modify the /etc/syslog.conf file. For example, if you are receiving a lot of log messages for a particular type of service (such as ppp if you are having trouble with a dial-up connection), you may consider directing messages for that service to its own log file. Then, if LogSentry uncovers a problem, it's easier to go through only that log file for those messages relating to the problem service.

Another temporary change you may consider is if you need to debug a problem with your system. Changing *.info to *.debug temporarily can give you more details on a problem. (Make sure to change it back later, or syslog will chew up too much system resources.)

## Using Password Protection

Passwords are the most fundamental security tool of any modern operating system and consequently, the most commonly attacked security feature. It is natural to want to choose a password that is easy to remember, but very often this means choosing a password that is also easy to guess. Crackers know that on any system with more than a few users, at least one person is likely to have an easily guessed password.

By using the “brute force” method of attempting to log in to every account on the system and trying the most common passwords on each of these accounts, a persistent cracker has a good shot of finding a way in. Remember that a cracker will automate this attack, so thousands of login attempts are not out of the question. Obviously, choosing good passwords is the first and most important step to having a secure system.

Here are some things to avoid when choosing a password:

- Do not use any variation of your login name or your full name. Even if you use varied case, append or prepend numbers or punctuation, or type it backwards, this will still be an easily guessed password.
- Do not use a dictionary word, even if you add numbers or punctuation to it.
- Do not use proper names of any kind.
- Do not use any contiguous line of letters or numbers on the keyboard (such as “qwerty” or “asdfg").

### Choosing good passwords

A good way to choose a strong password is to take the first letter from each word of an easily remembered sentence. The password can be made even better by adding numbers, punctuation, and varied case. The sentence you choose should have meaning only to you, and should not be publicly available (choosing a sentence on your personal Web page is a bad idea). Table 14-8 lists examples of strong passwords and the tricks used to remember them.

### Table 14-8: Ideas for Good Passwords

| Password | How to Remember it |
|:---------|:-------------------|
| Mrcl7yo! | My rusty car is 7 years old! |
| 2emBp1ib | 2 elephants make BAD pets, 1 is better |
| ItMc?Gib | Is that MY coat? Give it back |

The passwords look like gibberish, but are actually rather easy to remember. As you can see, I can place emphasis on words that stand for capital letters in the password. You set your password using the passwd command. Type the passwd command within a command shell, and it will enable you to change your password. First, it will prompt you to enter your old password. To protect against someone “shoulder surfing” and learning your password, the password will not be displayed as you type.

Assuming you type your old password correctly, the passwd command will prompt you for the new password. Once you type in your new password, the passwd command checks the password against cracklib to determine if it is a good or bad password. Non-root users will be required to try a different password if the one they have chosen is not a good password. The root user is the only user who is permitted to assign bad passwords. Once the password has been accepted by cracklib, the `passwd` command will ask you to enter the new password a second time to make sure there are no typos (which are hard to detect when you can’t see what you are typing). When running as root, it is possible to change a user’s password by supplying that user’s login name as a parameter to the `passwd` command. Typing this:

```
# passwd joe
```

results in the `passwd` command prompting you for joe’s new password. It does not prompt you for his old password in this case. This allows root to reset a user’s password when that user has forgotten it (an event that happens all too often).

## Using a shadow password file

In early versions of UNIX, all user account and password information was stored in a file that all users could read (although only root could write to it). This was generally not a problem because the password information was encrypted. The password was encrypted using a *trapdoor algorithm*, meaning the non-encoded password could be encoded into a scrambled string of characters, but the string could not be translated back to the non-encoded password.

How does the system check your password in this case? When you log in, the system encodes the password you entered, compares the resulting scrambled string with the scrambled string that is stored in the password file, and grants you access only if the two match. Have you ever asked a system administrator what the password on your account is only to hear, “I don’t know” in response? If so, this is why: The administrator really doesn’t have the password, only the encrypted version. The non-encoded password exists only at the moment you type it.

## Breaking encrypted passwords

There is a problem with people being able to see encrypted passwords, however. Although it may be difficult (or even impossible) to reverse the encryption of a trapdoor algorithm, it is very easy to encode a large number of password guesses and compare them to the encoded passwords in the password file. This is, in orders of magnitude, more efficient than trying actual login attempts for each user name and password. If a cracker can get a copy of your password file, the cracker has a much better chance of breaking into your system.

Fortunately, Linux and all modern UNIX systems support a shadow password file by default. The shadow file is a special version of the `passwd` file that only root can read. It contains the encrypted password information, so passwords can be left out of the `passwd` file, which any user on the system can read. Linux supports both the older, single password file method as well as the newer shadow password file. You should always use the shadow password file (it is used by default).

## Checking for the shadow password file

The password file is named `passwd` and can be found in the `/etc` directory. The shadow password file is named `shadow` and is also located in `/etc`. If your `/etc/shadow` file is missing, then it is likely that your Linux system is storing the password information in the /etc/passwd file instead. Verify this by displaying the file with the less command.

```
# less /etc/passwd
```

Something similar to the following should be displayed:

```
root:DkkS6Uke799fQ:0:0:root:/root:/bin/bash
bin:*:1:1:bin:/bin:
daemon:*:2:2:daemon:/sbin:

mary:KpRUp2ozmY5TA:500:100:Mary Smith:/home/mary:/bin/sh
joe:OsKrzvKnQaksI:501:100:Joe Johnson:/home/joe:/bin/sh
jane:ptNoIueYEjwX.:502:100:Jane Anderson:/home/jane:/bin/sh
bob:Ju2vY7A0X6Kzw:503:100:Bob Renolds:/home/bob:/bin/sh
```

Each line in this listing corresponds to a single user account on the Linux system. Each line is made up of seven fields separated by colon (: ) characters. From left to right the fields are the login name, the encrypted password, the user ID, the group ID, the description, the home directory, and the default shell. Looking at the first line, you see that it is for the root account and has an encrypted password of DkkS6Uke799fQ. We can also see that root has a user ID of zero, a group ID of zero, and a home directory of /root, and root's default shell is /bin/sh.

All of these values are quite normal for a root account, but seeing that encrypted password should set off alarm bells in your head. It confirms that your system is not using the shadow password file. At this point, you should immediately convert your password file so that it uses /etc/shadow to store the password information. You do this by using the pwconv command. Simply log in as root (or use the su command to become root) and enter the pwconv command at a prompt. It will print no messages, but when your shell prompt returns, you should have a /etc/shadow file and your /etc/passwd file should now look like this:

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:

mary:x:500:100:Mary Smith:/home/mary:/bin/sh
joe:x:501:100:Joe Johnson:/home/joe:/bin/sh
jane:x:502:100:Jane Anderson:/home/jane:/bin/sh
bob:x:503:100:Bob Renolds:/home/bob:/bin/sh
```

Encrypted password data is replaced with an x. Password data moved to /etc/shadow.

There is also a screen-oriented command called authconfig that you can use to manage shadow passwords and other system authentication information. This tool also has features that
