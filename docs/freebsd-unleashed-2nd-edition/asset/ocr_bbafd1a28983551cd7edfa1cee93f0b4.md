Crack reports only the users whose passwords were successfully guessed. In the sample output, the cracked passwords are shown in the first set of brackets; Frank's password is frank, and Joe's password is password—both very weak passwords that can be guessed by an attacker with little effort. You can then contact these users and remind them of the password policy, requiring them to change to stronger passwords.

Once you’re done running Crack, clean up the runtime tools and output files with the following two commands:

```
# make tidy
# rm run/F-merged
```

> **NOTE**
> 
> As FreeBSD continues to develop, it's highly likely that there will be support in the *passwd* program for automatic password-strength checking such as that done manually by *Crack*; in fact, the libraries that *Crack* uses are available at */usr/ports/security/cracklib*. On systems such as Linux, *cracklib* has been developed into a *Pluggable Authentication Module* (*PAM*), a mechanism that FreeBSD supports as well (see *man pam*), but FreeBSD doesn’t have *cracklib* support fully integrated into *PAM* as of this writing. For now, though, if you’re an adventurous sort willing to work with source code and experimental software, and you’re interested in incorporating the *cracklib* routines into the *passwd* program, you can learn how at *http://www.earney s.ca/-brent/FreeBSD/passwd42.html*.

# Forcing Password Expiration

By default, passwords in FreeBSD do not expire. However, one common part of a secure password policy is to require users to change their passwords every so often, with the expiration interval chosen by you.

To do this in FreeBSD, you need to modify the */etc/login.conf* file. This file controls system capabilities and behaviors, such as the number of allowed processes, the maximum allowed process size, the allowed number of simultaneous open files, and certain shell behaviors (learn more about this file in *man login.conf*). Each of these controls can be assigned to a “class” of users; you can assign users to classes with the *chfn* command (as you have seen in the “*The /etc/passwd and /etc/master.passwd Files*” section of Chapter 9, “Users, Groups, and Permissions”). By default, users aren’t associated with any particular class, so the values in the *default* class apply to everybody:

```
default:\
:passwd_format=md5:\
:copyright=/etc/COPYRIGHT:\
:welcome=/etc/motd:\
:setenv=MAIL=/var/mail/$,BLOCKSIZE=K,FTP_PASSIVE_MODE=YES:\
path=/sbin /bin /usr/sbin /usr/bin /usr/games /usr/local/sbin /usr/local/bin /usr/X11R6/bin /bin:\
```