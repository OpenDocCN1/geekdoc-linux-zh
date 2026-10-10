
## Creating a technical support mailbox

E-mail is a wonderful communication tool, especially for the overworked system administrator. People usually put more thought and effort into their e-mail messages than into their voicemail messages. A text message can be edited for clarity before being sent, and important details can be copied and pasted from other sources. This makes e-mail an excellent method for Linux users to communicate with their system administrators.

In an office with only a few users, you can probably get away with using your personal mailbox to send and receive support e-mails. In a larger office, however, you should create a separate mailbox reserved for technical support issues. This has several advantages over the use of your personal mailbox:

- Support messages will not be confused with personal, nonsupport-related messages.
- Multiple people can check the mailbox and share administrative responsibility without needing to read each other’s personal e-mail.
- Support e-mail is easily redirected to another person’s mailbox when you go on vacation. Your personal e-mail continues to go to your personal mailbox.

One easy solution is to simply create a support e-mail alias that redirects messages to an actual mailbox or list of mailboxes. For example, suppose you want to create a support alias that redistributes e-mail to the user accounts for support staff members Joe, Mary, and Bob. Log in as root, edit the `/etc/aliases` file, and add lines similar to the following:

```
# Technical support mailing list
support: joe, mary, bob
```

After saving the file, you need to run the `newaliases` command to recompile the `/etc/aliases` file into a database format. Now your users can send e-mail to the support e-mail address, and the message will be automatically routed to everyone on the list. When a member of the list responds to that message, he or she should use the Reply To All option so that the other support staff members also see the message. Otherwise, multiple people may attempt to solve the same problem, resulting in duplication of effort.

You may also choose to create a support user account. The technical support staff would log in to this account to check messages and send replies. In this manner, all replies are stamped with the support login name and not the personal e-mail address of a staff member.

## Resetting a user’s password

One common (if not *the* most common) problem that your users may encounter is the inability to log in because:

- They have the Caps Lock key on.
- They have forgotten the password.
- The password has expired.

If the Caps Lock key is not on, you probably need to reset the user’s password. You can’t look up the password because Linux stores hashed forms of passwords. Instead, use the `passwd` command to assign a new password to the user’s account. Give the user the new password (preferably in person), but then set the password to expire soon so that he or she must choose one (let’s hope one that is more easily remembered).

If you must reset a user’s password, do so with the `passwd` command. While logged in as root, type `passwd` followed by the login name you are resetting. You are prompted to enter the password twice. For example, to change the password for `mary`, type:

```
# passwd mary
```

After resetting the password, set it to expire so that the user will have to change it the next time she logs in. You can use the `chage` command to set an expiration period for the password and to trick the system into thinking that the password is long overdue to be changed.

```
# chage -M 30 -d 0 mary
```

The `-M 30` option tells the system to expire Mary’s password every 30 days. The `-d 0` option tricks the system into thinking that her password has not been changed since January 1, 1970. (Keep in mind that using `chage` activates password aging for any account on which it is used. Adding a `-1` to the `chage` command line disables password aging.)

> CROSS-REFERENCE: Administrators who support multiple users might want to consider some newer technologies that make life easier, such as centralized e-mail address books using LDAP. See Chapter 21 for more information.

# Modifying Accounts

Occasionally a user needs more done to an account than just a resetting of the password. You may need to change the groups that a user is in, the drive that a home directory resides on, or a person’s name changes because of new marital status. The following sections explain how to modify user accounts using one of two methods: `usermod` or the User Manager window.

## Modifying user accounts with usermod

The `usermod` command is similar to the `useradd` command and even has some of the same options. However, instead of adding new accounts, it enables you to change various details of existing accounts. When invoking the `usermod` command, you must provide account details to change followed by the login name of the account. Table 10-3 lists the available options for the `usermod` command.

### Table 10-3: usermod Options for Changing Existing Accounts

| Options | Description |
| :--- | :--- |
| `-a` | Adds user to the supplemental groups when used with the `-G` option. |
| `-c "comment"` | Changes the description field of the account. Non-root users can use the `chfn` command to change this field for themselves. Replace `comment` with a name or other description of the user account. Because the comment can contain multiple words, the quotation marks are necessary. |
| `-d home_dir` | Changes the home directory of the account to the specified new location. If the `-m` option is included, copy the contents of the home directory as well. Replace `home_dir` with the full path to the new directory. |
| `-e expire_date` | Assigns a new expiration date for the account, replacing `expire_date` with a date in the MM/DD/YYYY format. |
| `-f inactivity` | Sets the number of days after a password expires until the account is permanently disabled. Setting `inactivity` to 0 disables the account immediately after the password has expired. Setting it to -1 disables the option, which is the default behavior. |
| `-g group` | Changes the primary group (as listed in the `/etc/group` file) that the user is in. Replace `group` with the name of the new group. |
| `-G grouplist` | Sets the list of groups, besides the user's private group, that the user belongs to. Replace `grouplist` with a comma-separated list of groups. (If you don't use `-G` with the `-a` option, the user is removed from existing supplemental groups when the new ones are added.) |
| `-l login_name` | Changes the login name of the account to the name supplied after the `-l` option. Replace `login_name` with the new name. This does not automatically change the name of the home directory; use the `-d` and `-m` options for that. |
| `-L` | Locks a password and places a `!` in the password field. To lock an account, also set the expiration date to 1. |
| `-m` | This option is used only in conjunction with the `-d` option. It causes the contents of the user's home directory to be copied to the new directory. |
| `-o` | This option is used only in conjunction with the `-u` option. It removes the restriction that user IDs must be unique. |
| `-p passwd` | Enters a password for the account you are modifying. This must be an encrypted password. Instead of setting an encrypted password here, you can simply use the `passwd user` command later to add a password for user. The user should be asked to immediately change the password you set. |
| `-s shell` | Specifies a new command shell to use with this account. Replace `shell` with the full path to the new shell. |
| `-u user_id` | Changes the user ID number for the account. Replace `user_id` with the new user ID number. Unless the `-o` option is used, the ID number must not be in use by another account. |
| `-U` | Unlocks a user password. |
| `-Z SELinuxUser` | Defines the SELinux user for the user’s login. If no user is specified, the system picks the default SELinux user. |

Assume that a new employee named Jenny Barnes will be taking over Mary’s job. We want to convert the `mary` account to a new name (`-l jenny`), new comment (`-c "Jenny Barnes"`), and home directory (`-d /home/jenny`). You can do that with the following command:

```
# usermod -l jenny -c "Jenny Barnes" -m -d /home/jenny mary
```

Furthermore, if after converting the account you learn that Jenny prefers the `tcsh` shell, you can make that change with the `-s` option (`-s /bin/tcsh`):

```
# usermod -s /bin/tcsh jenny
```

Instead, you can use the `chsh` command to change the shell. The following is an example:

```
$ chsh -s /bin/tcsh jenny
```

The `chsh` command is handy because it enables a regular user to change his or her own shell setting to any shell listed in the `/etc/shells` file. (The root user can change his own shell to any command he chooses.) Simply leave the user name parameter off when invoking the command, and `chsh` assumes the currently logged-in user as the account to change.

Users can also change their own user information using the `chfn` command. This information is stored in the `/etc/passwd` file and displayed when you type the `finger` command (for example, `finger jenny`). In this example, the full name, office name, office phone, home phone, and work phone are set by the user `jenny`:

```
$ chfn -f "J Smith" -o "A-111" -p 555-1212 -h 555-2323 jenny
```

Users can also add information about themselves in the `.plan`, `.project`, `.forward`, and `.pgpkey` files in their home directory. That information will then be picked up by the `finger` command.

> **NOTE:** The `finger` command opens potential security issues. Finger gives out personal information that can be useful to those who want to crack your system. In addition, malicious users can flood your servers with finger requests.
