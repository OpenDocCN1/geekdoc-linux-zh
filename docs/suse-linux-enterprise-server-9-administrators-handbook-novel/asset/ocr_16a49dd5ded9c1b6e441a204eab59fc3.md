+   - **D** means the account is disabled and no SMB/CIFS logins will be allowed for this user.
+   - **W** means this account is a “Workstation Trust” account. This kind of account allows Windows workstations and servers to join a domain hosted by a Samba PDC.

The last field holds the time the account was last modified. It consists of the characters LCT= (Last Change Time) followed by a numeric encoding of the Unix time in seconds since the epoch (1970) that the last change was made. Any additional colon-separated fields after this LCT field are ignored.

# NOTE

All share names that end with a dollar sign ($) are hidden; they do not normally appear when a user displays server resources (such as using the NET VIEW \\SambaServername command from a Windows workstation). This also applies to such shares hosted on an SLES Samba server.

You can specify several options for each of the [share] sections. The most commonly used ones are as follows:

+   - `read only = yes/no` specifies whether the client can create, delete, or modify any files on the share. The default is `read only = yes`. (You can use `writable = yes` instead of `read only = no`.)
+   - `guest ok = yes/no` indicates whether a password is required to access this share. The default is `guest ok = no`, which means that a password is required. With `guest ok = yes`, it means that no password is required. (You can also use `public = yes`, an older and more vague form of `guest ok = yes`, and `public = no`, which is synonymous with `guest ok = no`.)
+   - `guest account = username` is the username that will be used to access services specified as `guest ok = yes`. The user must exist in the password file (or whatever service is used to authenticate the users). The default is nobody.
+   - `comment = description` provides a description of the nature of the share, which helps users to select the correct resource to access.
+   - `hosts allow = host1, host2, ...` specifies one or more machines that are allowed to access the share. The default is all hosts are granted access.
+   - `hosts deny = host1, host2, ...` specifies one or more machines that are not permitted to access the share. Localhost (127.0.0.1) is always granted access, but you can use `hosts deny = localhost` to block it.