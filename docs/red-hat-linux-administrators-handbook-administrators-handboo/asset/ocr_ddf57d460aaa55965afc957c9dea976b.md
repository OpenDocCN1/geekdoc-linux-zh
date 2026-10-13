+   3. After you locate the VNETSUP branch (for Windows 9x) or the Parameters branch (for Windows NT) in the Registry tree, select Edit→ New and choose to create a new DWORD value.
+   4. RegEdit will insert a new DWORD value called New Value #1 in the Registry. Rename this new value EnablePlainTextPassword and double-click this new name.
+   5. A dialog box pops, enabling you to set a value for the EnablePlainTextPassword you just created. Enter 1 as the value and close RegEdit as usual.
+   6. Reboot your Windows 9x/NT system.

This ensures that your Windows 9x/NT system is able to use plain-text passwords for SMB authentication.

# socket options

By default, the socket options parameter in the global configuration section is set to TCP_NODELAY, which enhances Samba performance on certain platforms. You should leave this parameter as is.

# dns proxy

This parameter affects how the Samba suite's built-in Windows Internet Name Server (nmbd) behaves when a Windows system name (NetBIOS name) cannot be resolved to an IP address. If you set this parameter to yes, the nmbd server will treat the NetBIOS names as an Internet domain name and try to resolve it by using the DNS protocol. Keeping the default setting is recommended.

# Setting the [homes] parameters

The [homes] section is a special configuration section that allows you to set up home directory access from Windows systems. In other words, a user with a valid username/password on the Red Hat system can access her home directory on the Linux system from a Windows system. The default [homes] configuration is as follows:

```
[homes]
    comment = Home Directories
```