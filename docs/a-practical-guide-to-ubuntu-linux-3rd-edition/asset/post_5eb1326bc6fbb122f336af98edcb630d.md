
## User_Alias

The alias_list for a user alias is the same as the user_list for a user privilege specification (discussed in the previous section). The following lines from a sudoers file define three user aliases: OFFICE, ADMIN, and ADMIN2. The alias_list that defines the first alias includes the usernames mark, sam, and sls; the second includes two usernames and members of the admin group; and the third includes all members of the admin group except Max.

- `User_Alias OFFICE = mark, sam, sls`
- `User_Alias ADMIN = max, zach, %admin`
- `User_Alias ADMIN2 = %admin, !max`

## Runas_Alias

The alias_list for a runas alias is the same as the runas_list for a user privilege specification (discussed in the previous section). The following SM runas alias includes the usernames sam and sls:

- `Runas_Alias SM = sam, sls`

## Host_Alias

Host aliases are meaningful only when the sudoers file is referenced by sudo running on more than one system. The alias_list for a host alias is the same as the host_list for a user privilege specification (discussed in the previous section). The following line defines the LCL alias to include the systems named dog and plum:

- `Host_Alias LCL = dog, plum`

If you want to use fully qualified hostnames (hosta.example.com instead of just hosta) in this list, you must set the fqdn flag (next section). However, doing so may slow the performance of sudo.

## Cmd_Alias

The alias_list for a command alias is the same as the command_list for a user privilege specification (discussed in the previous section). The following command alias includes three files and, by including a directory (denoted by its trailing /), incorporates all the files in that directory:

- `Cmd_Alias BASIC = /bin/cat, /usr/bin/vi, /bin/df, /usr/local/safe/`

# DEFAULTS (OPTIONS)

You can change configuration options from their default values by using the Defaults keyword. Most values in this list are flags that are implicitly Boolean (can either be on or off) or strings. You turn on a flag by naming it on a Defaults line, and you turn it off by preceding it with a !. The following line in the sudoers file would turn off the lecture and fqdn flags and turn on tty_tickets:

- `Defaults !lecture, !tty_tickets, fqdn`

This section lists some common flags; see the sudoers man page for a complete list.

- **env_reset**: Causes sudo to reset the environment variables to contain the LOGNAME, SHELL, USER, USERNAME, and SUDO_* variables only. The default is on. See the sudoers man page for more information.
- **fqdn** (fully qualified domain name): Performs DNS lookups on FQDNs (page 1149) in the sudoers file. When this flag is set, you can use FQDNs in the sudoers file, but doing so may negatively affect sudo’s performance, especially if DNS is not working. When this flag is set, you must use the local host’s official DNS name, not an alias. If hostname returns an FQDN, you do not need to set this flag. The default is on.
- **insults**: Displays mild, humorous insults when a user enters a wrong password. The default is off. See also passwd_tries.
- **lecture=freq**: Controls when sudo displays a reminder message before the password prompt. Possible values of freq are never (default), once, and always. Specifying lecture is the same as specifying a freq of never.
- **mail_always**: Sends email to the mailto user each time a user runs sudo. The default is off.
- **mail_badpass**: Sends email to the mailto user when a user enters an incorrect password while running sudo. The default is off.
- **mail_no_host**: Sends email to the mailto user when a user whose username is in the sudoers file but who does not have permission to run commands on the local host runs sudo. The default is off.
- **mail_no_perms**: Sends email to the mailto user when a user whose username is in the sudoers file but who does not have permission to run the requested command runs sudo. The default is off.
- **mail_no_user**: Sends email to the mailto user when a user whose username is not in the sudoers file runs sudo. The default is on.
- **mailsub=subj** (mail subject): Changes the default email subject for warning and error messages from the default `*** * * * SECURITY information for %h *** * * *` to subj. The sudo utility expands %h within subj to the local system’s hostname. Place subj between quotation marks if it contains shell special characters (page 160).
- **mailto=eadd**: Sends sudo warning and error messages to eadd (an email address; the default is root). Place eadd between quotation marks if it contains shell special characters (page 160).
- **passwd_tries=num**: The num is the number of times the user can enter an incorrect password in response to the sudo password prompt before sudo quits. The default is 3. See also insults and lecture.

# Using the root password in place of your password

> If you have set up a root password (page 431), you can cause graphical programs that require a password to require the root password in place of the password of the user who is running the program by turning on rootpw. The programs will continue to ask for your password, but will accept only the root password. Making this change causes an Ubuntu system to use the root password in a manner similar to the way some other distributions use this password.

- **rootpw**: Causes sudo to accept only the root password in response to its prompt. Because sudo issues the same prompt whether it is asking for your password or the root password, turning this flag on may confuse users. Do not turn on this flag if you have not unlocked the root account (page 431), as you will not be able to use sudo. To fix this problem, bring the system up in recovery mode (page 445) and turn off (remove) this flag. The default is off, causing sudo to prompt for the password of the user running sudo. See the preceding tip.
- **shell_noargs**: Causes sudo, when called without any arguments, to spawn a root shell without changing the environment. The default is off. This option is the same as the sudo -s option.
- **timestamp_timeout=mints**: The mints is the number of minutes that the sudo timestamp (page 423) is valid. The default is 15; set mints to -1 to cause the timestamp to be valid forever.
- **tty_tickets**: Causes sudo to authenticate users on a per-tty basis, not a per-user basis. The default is on.
- **umask=val**: The val is the umask (page 459) that sudo uses to run the command that the user specifies. Set val to 0777 to preserve the user's umask value. The default is 0022.

# Unlocking the root account (assigning a password to root)

Except for a few instances, there is no need to unlock the root account on an Ubuntu system; in fact, Ubuntu suggests that you do not do so. The following command unlocks the root account by assigning a password to it:

```bash
$ sudo passwd root
Enter new UNIX password:
Retype new UNIX password:
password: password updated successfully
```

- **Relocking the root account**: If you decide you want to lock the root account after unlocking it, give the command `sudo passwd -l root`. You can unlock it again with the preceding command.

# su: gives you another user's privileges

To use su to gain root privileges, you must unlock the root account (as discussed in the preceding section).

The su (substitute user) utility can spawn a shell or execute a program with the identity and privileges of a specified user. Follow su on the command line with the name of a user; if you are working with root privileges or if you know the user's password, you will then take on the identity of that user. When you give an su command without an argument, su defaults to spawning a shell with root privileges (you have to know the root password).

When you give an su command to work as root, su spawns a new shell, which displays the # prompt. You can return to your normal status (and your former shell and prompt) by terminating this shell: Press CONTROL-D or give an exit command. Giving an su command by itself changes your user and group IDs but makes minimal changes to the environment. For example, PATH has the same value as it did before
