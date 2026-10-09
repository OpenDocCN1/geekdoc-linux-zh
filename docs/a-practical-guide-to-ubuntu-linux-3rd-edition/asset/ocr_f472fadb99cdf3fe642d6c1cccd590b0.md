password, turning this flag on may confuse users. Do not turn on this flag if you have not unlocked the root account (page 431), as you will not be able to use sudo. To fix this problem, bring the system up in recovery mode (page 445) and turn off (remove) this flag. The default is off, causing sudo to prompt for the password of the user running sudo. See the preceding tip.

+   shell_noargs Causes sudo, when called without any arguments, to spawn a root shell without changing the environment. The default is off. This option is the same as the sudo -s option.

+   timestamp_timeout=mints The mints is the number of minutes that the sudo timestamp (page 423) is valid. The default is 15; set mints to -1 to cause the timestamp to be valid forever.

+   tty_tickets Causes sudo to authenticate users on a per-tty basis, not a per-user basis. The default is on.

+   umask=val The val is the umask (page 459) that sudo uses to run the command that the user specifies. Set val to 0777 to preserve the user's umask value. The default is 0022.

# Unlocking the root account (assigning a password to root)

Except for a few instances, there is no need to unlock the root account on an Ubuntu system; in fact, Ubuntu suggests that you do not do so. The following command unlocks the root account by assigning a password to it:

```
```
$ sudo passwd root
Enter new UNIX password:
Retype new UNIX password:
password: password updated successfully
```
```

+   Relocking the root account If you decide you want to lock the root account after unlocking it, give the command sudo passwd -l root. You can unlock it again with the preceding command.

# su: gives you another user's privileges

To use su to gain root privileges, you must unlock the root account (as discussed in the preceding section).

The su (substitute user) utility can spawn a shell or execute a program with the identity and privileges of a specified user. Follow su on the command line with the name of a user; if you are working with root privileges or if you know the user's password, you will then take on the identity of that user. When you give an su command without an argument, su defaults to spawning a shell with root privileges (you have to know the root password).

When you give an su command to work as root, su spawns a new shell, which displays the # prompt. You can return to your normal status (and your former shell and prompt) by terminating this shell: Press CONTROL-D or give an exit command. Giving an su command by itself changes your user and group IDs but makes minimal changes to the environment. For example, PATH has the same value as it did before