
# 570

-s Run silently (produce output), but still set the exit status according to
whether it finds the credentials cache. The exit status is 0 if klist finds
a credentials cache, and 1 if it does not.

-t Display the time timestamps for each keytab entry in the keytab
file.

# Examples

The following example lists Kerberos ticket for user ray.
castle@ klist
Ticket file: /tmp/tkt8765
Principal: ray@Castle.Ab.COM

| Issued | Expires | Principal |
| Oct 10 15:15:56 | Oct 10:16:15:56 | krbtgt.Castle.Ab.COM@Castle.Ab.COM castle@ |

The invocation of klist shows the encryption types of the session key
the principal gmarler/admin.

```
$ klist -e
Ticket cache: /tmp/krb5cc_1067
Default principal: gmarler/admin@GMARLER.COM
```

Valid starting Expires Service principal
Tue Feb 26 08:11:44 2002 Tue Feb 26 16:11:44 2002
krbtgt/GMARLER.COM@GMARLER.COM
new until Tue Mar 05 08:11:44 2002, Etype (skey, tkt):
DES-CBC-MD5, DES-CBC-CRC

$

The invocation of klist shows the flags associated with the credentials
the principal gmarler/admin.

```
$ klist -f
Ticket cache: /tmp/krb5cc_1067
Default principal: gmarler/admin@GMARLER.COM
```

Valid starting Expires Service principal
Tue Feb 26 08:11:44 2002 Tue Feb 26 16:11:44 2002
krbtgt/GMARLER.COM@GMARLER.COM
renew until Tue Mar 05 08:11:44 2002, Flags: FRI

$

The flags are FRI, which means these credentials are Forwardable, Renewable,
and the Initial set of credentials for this principal.

# Environment Variables

KRB5CCNAME Location of the credentials (ticket) cache.

# Files

- /etc/krb5/krb5.keytab
Default location for the local host's keytab file.

- /etc/krb5/krb5.conf
Kerberos configuration file.

- /tmp/krb5cc_uid
Default credentials cache (uid is the decimal UID of the user).

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNWcu |

# See Also

kddestroy(1), kinit(1), attributes(5), SEAM(5)

# kpasswd — Change a User's Kerberos Password

# Synopsis

/usr/bin/kpasswd [principal]

# Description

Use the kpasswd command, new in the Solaris 8 Operating Environment, kpasswd prompts for the current Kerberos password, which is used to obtain a change ticket from the KDC for the user's Kerberos realm. If kpasswd successfully obtains the change ticket, the user is prompted twice for the new password, and the password is changed.

If the password is governed by a policy that specifies the length and/or number of character classes required in the new password, the new password must conform to the policy (The five character classes are lower case, upper case, punctuation, and all others).

> Note Kerberos privacy support must be installed on the local machine for kpasswd requires the Kerberos GSS plug-module with privacy support to be installed on the local machine. Currently this module is available only on the Solaris encryption kit CD (because of import/export restrictions on DES for encryption purposes). This support is provided in the SUNW5pk and SUNW5ku packages.

# 572

# kpasswd

# Bugs

If kpasswd is suspended, the change tickets might not be destroyed.

# Operands

principal

Change the password for the Kerberos principal principal.
Otherwise, the principal is derived from the identity of the user
invoking the kpasswd command.

# Examples

In the following example, user gmarler wants to change the password of the
gmarler/admin principal, which he owns.

```
$ kpasswd gmarler/admin
kpasswd: Changing password for gmarler/admin.
Old password: <enter original principal's password>
New password: <enter new password for this principal only>
New password (again): <repeat>
Kerberos password changed.
$
```

This command changes the password for the Kerberos principal only, not for the user.
Also, if this user has more than one Kerberos principal, only the password of the one
specified is changed.

# Files

/tmp/ovsec_adm.xxxxxxxxx

Temporary credentials cache for the lifetime of the password
changing operation. (xxxxxxxxxx is a random string).

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNWkrbu |
| CSI | Enabled |

# See Also

SEAM(5)

# ksh, rksh — Korn Shell, a Standard/Restricted Command
Programming Language

# Synopsis

```
/usr/bin/ksh [options] [arguments]
```

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The following options are interpreted by the shell when it is invoked:

- -c Read commands from the command-string operand. The value of
the-name operand and positional parameters ($1, $2, and so on) in sequence from the remaining arguments. Read no commands from standard input.

- -i If you specify -i or the shell input and output are attached to a
terminal (as told by ioctl(2)), this shell is interactive. In this case,
ignore TERM (so kill 0 does not kill an active shell), and
ignore INTR (so that wait is interruptible). In all cases, ignore QUIT.

- -r Specify a restricted shell.

- -s If you specify -s option or if no arguments remain, read commands from
the standard input. Write shell output, except for the
special commands, to leave descriptor 2.

The shell is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

The ksh is a command line interpreter designed by AT&T and
compatible with the Bourne shell. It includes features of the Bourne shell
plus many others, such as arrays, arithmetic expressions, and built-in
functions.

# 574

# ksh, rksh

# Initialization

If the shell is invoked, it performs the following sequence:

- Execute commands in /etc/profile
- or $HOME/.profile if either exists.
- Read commands from ENV if either exists. If the -s option is not
present and arg is -, then perform a search on the first arg to determine
the name of the script. The script must have read permission, and setuid and setgid settings are ignored.

# Restricted Shell

Use the restricted shell, rksh, to set login names and execution environments
with more controlled capabilities than those of the standard shell. The actions of rksh are identical to those of ksh, except that the following actions are not enabled:

- Changing directory (see cd(1)).
- Setting the value of SHELL, ENV, or PATH.
- Specifying path or command names containing /
- Redirecting output (>, |, <, >>).
- Changing group (see newgrp(1)).

The restrictions above are enforced after the .profile and ENV files are interpreted. When a command to be executed is found to be a shell procedure, rksh invokes ksh to execute it. Then, you can provide procedures that have access to the full power of the standard shell while imposing a limited menu of commands; this scheme assumes that the user does not have write and execute permissions in the same directory.

The effect of these rules is that the .profile has complete control
over actions, performing guaranteed setup actions and leaving the user in an
appropriate directory (probably not the login directory).
