```
# chage -I 7 joe
# chage -m 7 joe
# chage -M 7 joe
# chage -W 3 joe
Grace period 1 week from password expiry
Like passwd -m
Like passwd -x (Grr, grr.)
Like passwd -w (Grr, grr.)
```

(chage can change all settings that passwd can change, and then some.)

If you cannot remember the option names, invoke chage with the name of a user account only. The program will present you with a sequence of the current values to change or confirm.

You cannot retrieve a clear-text password even if you are the administrator. Even checking /etc/shadow doesn’t help, since this file stores all passwords already encrypted. If a user forgets their password, it is usually sufficient to reset their password using the passwd command.

Should you have forgotten the root password and not be logged in as root by any chance, your last option is to boot Linux to a shell, or boot from a rescue disk or CD. After that, you can use an editor to clear the (password) field of the root entry in /etc/passwd.

# Exercises

+   1. **13.7** [3] Change user joe’s password. How does the /etc/shadow file change? Query that account’s password state.

+   2. **13.8** [2] The user dumbo has forgotten his password. How can you help him?

+   3. **13.9** [5] Adjust the settings for user joe’s password such that he can change his password after at least a week, and must change it after at most two weeks. There should be a warning two days before the two weeks are up. Check the settings afterwards.

# 13.3.3 Deleting User Accounts

To delete a user account, you need to remove the user’s entries from /etc/passwd and /etc/shadow, delete all references to that user in /etc/group, and remove the user’s home directory as well as all other files created or owned by that user. If the user has, e. g., a mail box for incoming messages in /var/mail, that should also be removed.

Again there is a suitable command to automate these steps. The userdel command removes a user account completely. Its syntax:

```
userdel [-r] <user name>
```

The -r option ensures that the user’s home directory (including its content) and his mail box in /var/mail will be removed; other files belonging to the user—e. g., cron tab files—must be delete manually. A quick way to locate and remove files belonging to a certain user is the

```
find / -uid <UID> -delete
```

command. Without the -roption, only the user information is removed from the user database; the home directory remains in place.