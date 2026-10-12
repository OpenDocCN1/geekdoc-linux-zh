# passwd-check

This keyword defines the type of passwords required for anonymous users. The default setting requires the password for an anonymous access to be an e-mail address but does not enforce this rule if the user fails to enter a valid e-mail address. The server just warns the user about the invalid password.

**Syntax:** `passwd-check none|trivial|rfc822 (enforce|warn)`

**Default:** `passwd-check rfc822 warn`

When you don’t want password checking, set the passwd-check keyword as follows:

```
passwd-check none
```

If you set the checking to be trivial, the server checks only for the existence of an @ character in the password.

# path-filter

This keyword enables you to restrict certain filenames, specifically those used in file uploads by users specified in typelist.

**Syntax:** `path-filter typelist mesg allowed_charset {disallowed regexp . . .}`

# upload

This keyword allows you to enable or disable an upload directory.

**Syntax:** `upload root_dir dirglob yes|no owner group`

For example, the following directive enables the /dropbox directory as an upload directory where files are owned by root and the group ownership is set to ftp:

```
upload /home/ftp /dropbox yes root ftp 0600
```

The uploaded files have a permission setting of 0600. Note that /home/ftp must be the home directory of the user ftp. If the uploader should not be allowed to create new subdirectories under the /dropbox directory, then the preceding upload line needs to be changed to:

```
upload /home/ftp /dropbox yes root ftp 0600 nodirs
```

On the other hand, if the uploader should be allowed to create subdirectories, then nodirs can be replaced with dirs.