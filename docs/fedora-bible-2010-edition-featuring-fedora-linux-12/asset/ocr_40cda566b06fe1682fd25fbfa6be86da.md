# Table 10-2: useradd Options for Changing User Defaults

| Options | Description |
|---|---|
| `-b` `default_home` | Sets the default directory in which user home directories will be created. Replace `default_home` with the directory name to use. Usually this is `/home`.
| `-e` `default_expire_date` | Sets the default expiration date on which the user account is disabled. The `default_expire_date` value should be replaced with a date in the form MM/DD/YYYY \u2014 for example, 10/15/2010. |
| `-f` `default_inactive` | Sets the number of days after a password has expired before the account is disabled. Replace `default_inactive` with a number representing the number of days. |
| `-g` `default_group` | Sets the default group in which new users will be placed. In Fedora, `useradd` creates a new group with the same name and ID number as the user, so this value is ignored. To set a different group primary group for a user, you must set it explicitly with the `-g` option on the command line. |
| `-s` `default_shell` | Sets the default shell for new users. Typically this is `/bin/bash`. Replace `default_shell` with the full path to the shell that you want as the default for new users. |

To set any of the defaults, give the `-D` option first, then add any of the defaults you want to set. For example, to set the default home directory location to `/home/everyone` and the default shell to `/bin/tcsh`, type the following:

```
```
# useradd -D -b /home/everyone -s /bin/tcsh
```
```

Besides setting up user defaults, an administrator can create default files that are copied to each user’s home directory for use. These files can include login scripts and shell configuration files (such as `.bashrc`). The following sections describe some of these files.

# Supplying initial login scripts

Many Linux applications, including the command shell itself, read a configuration file at startup. Typically these configuration files are stored in the users’ home directories. In this way, each user can customize the behavior of the command shell and other applications without affecting that behavior for other users. In this way, global defaults can be assigned from `/etc/profile`, and then those settings can be customized by a user’s personal files.

The `bash` command shell, for example, looks for a file called `.bashrc` in the current user’s home directory whenever it starts up. Similarly, the `tcsh` command shell looks for a file called `.cshrc` in the user’s home directory. You may see a repeating theme here. Startup scripts and configuration files for various applications usually begin with a dot (`.`) character and end in the letters `rc` (which stands for `run commands`). You can supply initial default versions of these and other configuration files by placing them in the `/etc/skel` directory.