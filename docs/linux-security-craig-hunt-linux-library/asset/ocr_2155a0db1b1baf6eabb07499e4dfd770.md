**NOTE** If your remote SMB server is a Windows NT server, domain mode access control is always preferable to server mode because server mode consumes a license on the Windows NT server for the duration of the client-server connection. domain mode authentication, on the other hand, releases the connection (and the Windows NT license instance) as soon as the authentication is performed. This is important because Microsoft's licensing strategy revolves around concurrent server connections.

# Other Access Control Features

In addition to these four access control methods, you may choose to take advantage of a trust relationship between your local NT domain and a second, trusted NT domain. As of Samba 2.0.4, the `smb.conf` directive `allow trusted domain = yes` can be used to gain authentication from an NT domain controller that, although it is not primary to your domain, is trusted by your PDC.

Another recent addition to the access control feature set of Samba is the `add user script` directive. This can be used in both `user` and `domain` access control modes to automatically add a user in the event that the user/password is authenticated by the password server but the user is not present locally. For example, you may want Samba to automatically add a user locally using the following `smb.conf` directive:

```
```text
add user script = sudo /usr/sbin/useradd %u
```
```

Conversely, a `delete user script` directive can be specified to delete a user that exists locally but is no longer valid on the PDC. An example of this usage is as follows:

```
```text
delete user script = sudo /usr/sbin/userdel %u
```
```

While adding and deleting local users in this fashion may be convenient, I urge you to implement it carefully because you are allowing the unattended creation and deletion of users in the same `/etc/passwd` or `/etc/shadow` files that you use for regular Linux server authentication.

# The [homes] Directive

A common approach to allowing all Linux server users access to their home directories is the special `[homes]` directive in the `smb.conf` file. Consider the following example:

```
```text
[homes]
comment = Home Directories
browseable = no
writable = yes
```
```

This directive specifies that any user in `/etc/passwd` can gain access to their home directory by pointing their SMB client to `\\server\\username`. This is not always desirable