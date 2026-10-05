# Chapter 13 - Creating Users and Groups

| Option name | Option abbreviation | Effect |
| --- | --- | --- |
| --skel skeleton-dir | -k | Normally, default user configuration files are copied from /etc/skel, you may specify another template with this option, which is valid only in conjunction with -m. |
| None | -M | This option forces the system not to automatically create a home directory. |
| --shell shell | -s | You set the name of the user's default login shell with this option. The default is /bin/bash. |
| --uid UID | -u | This parameter creates an account with the specified user ID (UID). |
| --non-unique | -o | This parameter enables a single UID number to be reused; this option is passed when creating the second or subsequent account that uses a UID. |
| --system | -r | This parameter specifies the creation of a system account for system accounts, and gives them UID values below 100. |
| --no-user-group | -N | This option disables creation of a group for the user |

You can add a password with the useradd -p option. However, for security reasons, this is not recommended. It is better to use the passwd command, as described later in this chapter.

Some of these options aren't readily accessible when creating accounts GUI tools, but the details differ from one GUI utility to another. In some cases, options can be set in a GUI utility after the account has been created, but not when creating it.

You might want to specify a UID to keep these values synchronized across computers that share files with the Network File System (NFS), which identifies file ownership via UIDs.

A complete useradd command, including setting a few options, like this:

```
$ sudo useradd -m -c "Samantha Bresnanhan" -u 1012 samantha
's password:
```

This creates an account with a username samantha, a home directory, comment field containing the user's full name, and a UID of 1012. In the preceding example that the sudo command was used to obtain superuser privileges, required to complete this command successfully. If you were logged into the root account. sudo would not be needed.