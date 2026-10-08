
```
72: Unknown command: .BR
84: Unknown command: .BI
88: Unknown command: .BI
90: Unknown command: .BR
96: Unknown command: .BR
116: Unknown command: .BI
120: Unknown command: .SB
122: Unknown command: .BR
131: Unknown command: .SB
133: Unknown command: .BR
135: Unknown command: .RB
137: Unknown command: .BI
144: Unknown command: .BR
156: Unknown command: .BR
157: Unknown command: .BR
158: Unknown command: .BR
159: Unknown command: .BR
160: Unknown command: .BR
161: Unknown command: .BR
137: Unmatched \f1
116: Unmatched \f1
castle%
```

The following example uses the -a option to suppress the Unknown command messages for .BI and .BR.

```
castle% checknr -a.BI.BR checknr.1
62: Unknown command: .SB
64: Unmatched .SB
54: Unmatched \f3
54: Unmatched \f2
54: Unmatched \f1
54: Unmatched \f3
54: Unmatched \f1
57: Unmatched \f3
57: Unmatched \f2
57: Unmatched \f1
57: Unmatched \f3
57: Unmatched \f1
120: Unknown command: .SB
131: Unknown command: .SB
135: Unknown command: .RB
137: Unmatched \f1
116: Unmatched \f1
castle%
```

## Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNdoc |

## chgrp

### See Also

- eqn(1), nroff(1), troff(1), attributes(5), me(5), ms(5)

## chgrp — Change File Group Ownership

### Synopsis

```
/usr/bin/chgrp [-f -R] group file
```

### Description

You can use the chgrp command to change the group that owns a file, provided that you own the file and you are a member of the group that owns it. The chgrp command sets the group ID of the file named by each file operand to the group ID specified by the chgrp operand.

For each operand, chgrp performs actions equivalent to the chown(2) function, called with the following arguments:

- The file operand is used as the path argument.
- The user ID of the file is used as the owner argument.
- The specified group ID is used as the group argument.

Unless chgrp is invoked by a process with appropriate privileges, the set-user-ID and set-group-ID bits of all file groups are cleared upon successful completion; the set-user-ID and set-group-ID bits of other file types may be cleared.

The operating system has a {_POSIX_CHOWN_RESTRICTED} configuration option to restrict ownership changes. When this option is in effect, the owner of the file can change the group of the file only to a group to which the owner belongs. Only the superuser can arbitrarily change owner IDs, regardless of whether this option is in effect. To set this option, include the following line in /etc/system:

```
chown = 1
```

To disable this option, include the following line in /etc/system:

```
chown = 0
```

{POSIX_CHOWN_RESTRICTED} is enabled by default. See system(2) and pathconf(2).

### Options

- -f Do not report errors.
- -h If the file is a symbolic link, change the group of the symbolic link. Without this option, change the group of the file referenced by the link.
- -R Recursively descend through the directory and any subdirectories, setting the specified group ID as chgrp proceeds. When chgrp encounters a symbolic link, change the group of the target file (unless you specify -h), but no recursion.

### Operands

A group name from group or a numeric group ID. Either specifies a group ID given to file named by one of the operands. If a numeric group operand exists in group database as a group name, the group ID associated with that name is used as the group ID.

A path name of a file whose group ID is to be modified.

### Usage

usage(5) for the description of the behavior of chgrp when encountering files greater or equal to 2 bytes.

### Examples

In the following example, the owner of the file changes the group for the file named try to other.

```
chgrp other try
ls -l -rw-rw- 1 other Aug 27
```

In the following example, user ray tries to change the group for the file named try to staff but does not own the file. An error message is displayed.

```
chgrp whoami ray
chgrp staff try
chgrp: Not owner
```

In the following example, superuser changes the group for the file named try back to staff.

```
chgrp su
Password:
chgrp staff try
ls -l -rw-rw- 1 staff Aug 27
```

### Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of chgrp: LC_CTYPE, LC_MESSAGES, and LCPATH.

### Exit Status

- 0 The command executed successfully, and all requested changes were made.
- 1 An error occurred.

## Files

/etc/group Group file.

## Attributes

Use attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | Enabled |

Note - chgrp is enabled except for the group name.

### See Also

- chmod(1), chown(1), id(1), chown(2), pathconf(2), group(4), passwd(4), system(4), attributes(5), environ(5), file(5)

## chkey — Change User's Secure RPC Key

### Synopsis

```
/usr/bin/chkey [-p] [-s nisplus | nis | files] [-m mechanism]
```

### Description

Use chkey to change a user's secure RPC key and secret key. chkey prompts for the old RPC password and verifies that it is correct by decrypting the secret if the user has not already logged in, chkey registers the secret with the local keyserver(1) daemon. If the RPC password does not match the login password, chkey prompts for the login password. chkey uses the login password to encrypt the user's Diffie-Hellman (192-bit) cryptographic key.

chkey ensures the login password and the secure RPC password are kept the same, enabling password shadowing (see shadow(4)).

The key may be stored in /etc/publickey file (see publickey(4)), NIS public key map, or the NIS+_dir file. If a new key is generated, it is registered with the local keyserver(1).

You can change or replace secret mechanisms with the -option followed by the authentication mechanism name. You can use multiple -options to change one or more keys. However, only mechanisms configured in nsswitch.conf(1) can be changed with chkey.

If you do not specify the source of the public key with the -s option, chkey consults the public key entry in the name service switch configuration file (conf). If the entry specifies only one source, then chkey changes the key in the specified service name. However, if multiple services are listed, chkey cannot decide which source to use and displays an error message.

Specify the source explicitly with the -s option. Non-root users are not allowed to change their key pair in the files database.

## Files

/etc/nsswitch.conf conf

## chmod

### Options

- -p Reencrypt the existing secret key with the user's login password.
- -s nisplus Update the NIS+ database.
- -s nis Update the NIS database.
- -s files Update the files database.
- -m mechanism Change or reencrypt the secret key for the specified mechanism.

### Examples

The following example changes the NIS secure RPC key pair for user ray.

```
child$ chmod -p
Updating nie publickey database.
Reencrypting key for unix.1002@Castle.Ab.COM
please enter the Secure-RPC password for ray:
Please enter the login password for ray:
child$ ls -l -rw-rw- 1 ray Aug 27
```

## Files

/etc/publickey file

## Attributes

Use attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | Enabled |

### See Also

- login(1), logout(1), newkey(1), addcred(1), switchconf(4), shadow(4), attributes(5)

## chmod — Change the Permissions Mode of a File

### Synopsis

```
/usr/bin/chmod [-f R] absolute-mode file...
/usr/bin/chmod [-f R] symbolic-mode-list file...
```

### Description

chmod (change mode) command to change the mode of a file. The mode of a file specifies its permissions and other attributes. You can specify the mode in one of two ways: absolute or symbolic.

### Absolute Mode

You specify an absolute mode in octal numbers by using the following syntax:
chmod [options] absolute-mode file...

where you specify absolute mode with nnn, where n is a number from 0 to 7. You construct an absolute mode from the OR of any of the following modes:

- 4000 Set user ID
- 2000 Set group ID on execution if 7, 5, 3, or 1. Enable mandatory locking if #6, 4, 2, or 0. For directories, create BSD semantics for propagation of the group ID. With this option, files and subdirectories created in the directory inherit the group ID of the directory instead of the current process. You can clear the group ID only by using symbolic mode.
- 1000 Turn on sticky bit. See chmod(2).
- 0400 Allow read by owner.
- 0200 Allow write by owner.
- 0100 Allow execute (search in directory) by owner.
- 0700 Allow read, write, and execute (search) by owner.
- 0040 Allow read by group.
- 0020 Allow write by group.
- 0010 Allow execute (search in directory) by group.
- 0070 Allow read, write, and execute (search) by group.
- 0004 Allow read by others.
- 0002 Allow write by others.
- 0001 Allow execute (search in directory) by others.
- 0007 Allow read, write, and execute (search) by others.

> Note — You cannot set or clear the setgid bit in absolute mode; you must set (or clear) it in symbolic mode, using g+s (or g-s).

### Symbolic Mode

You specify a symbolic mode by using the following syntax:
chmod [options] symbolic-mode-list file...

where symbolic-mode-list is a comma-separated list (with no intervening space) of symbolic mode expressions of the form:

```
[who] operator [permissions]
```
