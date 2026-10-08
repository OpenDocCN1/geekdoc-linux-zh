
/* If the following parser is one created by lex, the
application must be careful to ensure that LC_CTYPE
and LC_COLLATE are set to the POSIX locale. */
(void) yyparse();
    return (0);
}

#include <stdio.h>
int yerrror(const char *msg)
{
    (void) fprintf(stderr, "%s\n", msg);
    return (0);
}
```

The following example draws yacc rules from the grammar.y file and puts the output
y y.tab.c.
castle% yacc grammar.y

The following example draws yacc rules from the grammar.y file and puts the output
y in.tab.c. It also produces the y.tab.h file, which would contain C-style #define
statements for the tokens defined in the grammar.y file.
castle% yacc -d grammar.y

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the
execution of yacc: LC_CTYPE, LC_MESSAGES, and NLSPATH.
yacc can handle characters from Extended UNIX Code (EUC) primary and
supplementary code sets as one-token symbols. EUC codes can be only single-character
quoted terminal symbols. yacc expects yylex() to return a wide-character (wchar_t)
value for these one-token symbols.

# Exit Status

-   0 Successful completion.
- >0 An error occurred.

# Files

-   y.output State transitions of the generated parser.
- y.tab.c Source code of the generated parser.
- y.tab.h Header file for the generated parser.
- yacc.acts Temporary file.
- yacc.debug Temporary file.
- yacc.tmp Temporary file.
- yaccpar Parser prototype for C programs.

# yes 1573

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|--- | --- |
| Availability | SUNwtool |

# See Also

-   lex(1), cc(1B), attributes(5), environ(5)
Programming Utilities

# Diagnostics

The number of reduce-reduce and shift-reduce conflicts is reported on the standard error output. You can find a more detailed report in the y.output file. Similarly, if some errors are not reachable from the start symbol, this instance is also reported.

# yes — Generate Repetitive Affirmative Output

# Synopsis

/bin/yes [expletive...]

# Description

You can use the yes command, new in the Solaris 9 Operating Environment, to respond programmatically to programs that require an interactive response.

Use the yes command to repeatedly output y, or if you specify expletive it is repeatedly followed by a newline. Multiple arguments are output separated by spaces and followed by a newline. To terminate, type an interrupt character.

# Examples

The following example shows the default output of the yes command.

```
mpoke% yes
y
y
y
...
Ctrl-C
mpoke%
```

The following example shows the output of the yes command when you specify an expletive of goodgrief.

```
mpoke% yes goodgrief
goodgrief
goodgrief
goodgrief
...
```

# 1574

# ypcat

Ctrl-C
mopoke%

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNmesu |

# See Also

-   - attributes(5)

# ypcat — Print Values in an NIS Database

# Synopsis

```
/usr/bin/ypcat [-kx] -d ypdomain mname
```

# Description

The ypcat command prints values in the NIS name service map specified by mname, which may be either a map name or a map nickname. Because ypcat uses the NIS network services, you need not to specify an NIS server.

Refer to ypfiles(4) for an overview of the NIS name service.

# Options

-   -d ypdomain

Specify a domain other than the default domain.

-   -k Display the keys for those maps in which the values are null or the key is not part of the value. None of the maps derived from file that have an ASCII value in /etc fall into this class.

-   -x Display map nicknames.

# Examples

The following example shows the output of the ypcat -x command on a system that is not on an NIS+ network.

```
castle% ypcat -x
Use "passwd" for map "passwd.byname"
Use "group" for map "group.byname"
Use "networks" for map "networks.byaddr"
Use "hosts" for map "hosts.byname"
Use "protocols" for map "protocols.bynumber"
Use "services" for map "services.byname"
Use "aliases" for map "mail.aliases"
```

# ypmatch 1575

Use "ethers" for map "ethers.byname"
castle%

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwhisu |

# See Also

ypmatch(1), ypfiles(4), attributes(5)

# ypmatch — Print the Value of Keys from an NIS Map

# Synopsis

```
/usr/bin/ypmatch [-k] [-t] [-d domain] key [key...] mname
/usr/bin/ypmatch -x
```

# Description

ypmatch prints the values associated with one or more keys from the NIS name services map specified by mname, which may be either a map name or a map nickname.
You can specify multiple keys. All keys are searched for in the same map. The keys must be the same case and length. No pattern matching is available. If a key is not matched, a diagnostic message is displayed.

> Note — ypmatch fails with an RCP error message on yp operations if enough file descriptors are not available. If this problem occurs, increase the number of file descriptors.

# Options

-   -d domain Specify a domain other than the default domain.
- -k Before printing the value of a key, print the key itself, followed by a colon (:).
- -t Inhibit map nickname translation.
- -x Display the map nickname table. This option lists the nicknames (names) the command knows and indicates the map name associated with each nickname.

# Operands

-   mname The NIS name services map.

# 1576

# ypppasswd

# Exit Status

- 0 Successful completion.
-1 An error occurred.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwhisu |

# See Also

ypcat(1), ypfiles(4), attributes(5)

# ypppasswd — Change Your Password in NIS

# Synopsis

```
/usr/bin/yppasswd [username]
```

# Description

> Note — The use of ypppasswd is discouraged, as it is now a link to passwd(1), which you should use.

The NIS password changes the password associated with the user in NIS Service. If you omit the domain, the password may be different from the local one.

ypppasswd prompts for the old password and then the new password. New passwords must be at least four characters long if use use a alphabet, and at least six characters if mostly. These rules are relaxed if you are superuser.

 the the the the password to take effect.

The NIS daemon, rpc.ypppasswd, must be running on your server for the password to take effect.

# ypwich 1577

> **Warning** — Even after you have changed your password using this command, the subsequent login(1) is successful only if password is obtained from NIS. (See getpwnam(3C), getspnam(3C), and nswitch.conf(4))

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | Sunwhiso |

# See Also

keylogin(1), login(1), nispasswd(1), passwd(1), getpwnam(3C), getspnam(3C), secure_rpc(3NS), nswitch.conf(4), attributes(5)

# Bugs

The update protocol passes all information to the server in RPC call without looking at it. Thus, if you type your old password incorrectly, you are not notified until you have entered your new password.

# ypwich — Return Name of NIS Server of Map Master

# Synopsis

```
/usr/bin/ypwich [-d domain] [[-t] -m [nname]] | [-Vn] hostname
/usr/bin/ypwich -x
```

# Description

ypwich returns the name of the NIS server that supplies the NIS names to an NIS client or that is the map. If invoked without arguments, ypwich gives the NIS server for the local system. If you specify hostname, that system is queried to find out which NIS server it is using.

Refer to ypfiles(4) for an overview of the NIS name services.

# Options

-   -d domain Use domain instead of the default domain.

-   -m mname Find the NIS server for a map. You cannot specify a host name with -m mname can be a map name or a nickname for a map. When you omit mname, produce a list of available maps.

-   -t Inhibit map nickname translation.

-   -Vn Version of ypbind: V3 is the default.

-   -x Display the map nickname translation table.
