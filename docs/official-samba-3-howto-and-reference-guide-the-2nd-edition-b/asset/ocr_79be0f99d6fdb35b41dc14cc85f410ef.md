Samba promptly when a security vulnerability is discovered. Check with your OS vendor for OS-specific upgrades.

# 17.5    Common Errors

If all Samba and host platform configurations were really as intuitive as one might like them to be, this chapter would not be necessary. Security issues are often vexing for a support person to resolve, not because of the complexity of the problem, but because most administrators who post what turns out to be a security problem request are totally convinced that the problem is with Samba.

# 17.5.1    Smbclient Works on Localhost, but the Network Is Dead

This is a common problem. Linux vendors tend to install a default firewall. With the default firewall in place, only traffic on the loopback adapter (IP address 127.0.0.1) is allowed through the firewall.

The solution is either to remove the firewall (stop it) or modify the firewall script to allow SMB networking traffic through. See Section 17.3.4 section.

# 17.5.2    Why Can Users Access Other Users’ Home Directories?

> “We are unable to keep individual users from mapping to any other user's home directory once they have supplied a valid password! They only need to enter their own password. I have not found any method to configure Samba so that users may map only their own home directory.”

> “User xyzzy can map his home directory. Once mapped, user xyzzy can also map anyone else’s home directory.”

This is not a security flaw, it is by design. Samba allows users to have exactly the same access to the UNIX file system as when they were logged on to the UNIX box, except that it only allows such views onto the file system as are allowed by the defined shares.

If your UNIX home directories are set up so that one user can happily `cd` into another user’s directory and execute `ls`, the UNIX security solution is to change file permissions on the user’s home directories so that the `cd` and `ls` are denied.

Samba tries very hard not to second guess the UNIX administrator’s security policies and trusts the UNIX admin to set the policies and permissions he or she desires.

Samba allows the behavior you require. Simply put the *only user = %S* option in the */homes/* share definition.

The *only user* works in conjunction with the *users* = list, so to get the behavior you require, add the line:

```
```text
users = %S
```
```