-l-llogfile=logdirectory  Base directory name for log/debug files. The extension ".progname" will be appended (c.g.  log.smbclient, log.smbd, etc... ). The log file is never removed by the client.

# ACL FORMAT

The format of an ACL is one or more ACL entries separated by either commas or newlines. An ACL entry is one of the following:

```
```
REVISION:<revision number>
OWNER:<sid or name>
GROUP:<sid or name>
ACL:<sid or name>:<type>/<flags>/<mask>
```
```

The revision of the ACL specifies the internal Windows NT ACL revision for the security descriptor. If not specified it defaults to 1. Using values other than 1 may cause strange behaviour.

The owner and group specify the owner and group sids for the object. If a SID in the format S-1-x-y-z is specified this is used, otherwise the name specified is resolved using the server on which the file or directory resides.

ACLs specify permissions granted to the SID. This SID again can be specified in S-1-x-y-z format or as a name in which case it is resolved against the server on which the file or directory resides. The type, flags and mask values determine the type of access granted to the SID.

The type can be either 0 or 1 corresponding to ALLOWED or DENIED access to the SID. The flags values are generally zero for file ACLs and either 9 or 2 for directory ACLs. Some common flags are:

+   -   `#define SEC_ACE_FLAG_OBJECT_INHERIT 0x1`
+   -   `#define SEC_ACE_FLAG_CONTAINER_INHERIT 0x2`
+   -   `#define SEC_ACE_FLAG_NO_PROPAGATE_INHERIT 0x4`
+   -   `#define SEC_ACE_FLAG_INHERIT_ONLY 0x8`

At present flags can only be specified as decimal or hexadecimal values.

The mask is a value which expresses the access right granted to the SID. It can be given as a decimal or hexadecimal value, or by using one of the following text strings which map to the NT file permissions of the same name.

+   -   *R* - Allow read access
+   -   *W* - Allow write access
+   -   *X* - Execute permission on the object