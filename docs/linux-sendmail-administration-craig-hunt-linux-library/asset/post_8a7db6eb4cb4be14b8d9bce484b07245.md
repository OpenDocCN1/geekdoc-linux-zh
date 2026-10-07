
# Table A.1 Sendmail m4 Macros and Configuration Commands (continued)

| Command | Usage |
|---|---|
| GENRICS_DOMAIN_FILE | Identifies a file that lists fully qualified domains that should be converted by the generic database. | |
| HACK | Selects a file containing a locally defined temporary fix. |
| INPUT_MAIL_FILTER | Defines a mail filter and the variables necessary to call the filter. |
| LDAPOUTE_DOMAIN | Defines a domain for which mail should be routed based on an LDAP directory entry. |
| LDAPOUTE_DOMAIN_FILE | Identifies a file that lists domains for which mail should be routed based on entries in an LDAP directory. |
| LOCAL_CONFIG | Marks the start of a section that contains raw sendmail.cf commands. |
| LOCAL_DOMAIN | Defines an alias hostname for the mail server. |
| LOCAL_NET_CONFIG | Marks the start of raw rewrite rules that define how mail destined for the local network is handled. |
| LOCAL_RULE_n | Marks the start of a section that contains raw rewrite rules. The $n$, which must be 0, 1  2, or 3, identifies the ruleset to which the rewrite rules are added. |
| LOCAL_RULESETS | Marks the start of a ruleset to be added to the configuration. |
| LOCAL_USER | Lists usernames that should be exempted from relating when local mail is being relayed. |
| MAIL_FILTER | Defines a mail filter. |
| MAILER | Identifies a set of mailers to be included in the sendmail.cf file. |

# Table A.1 Sendmail m4 Macros and Configuration Commands (continued)

| Command | Usage |
| --- | --- |
| MAILER_DEFINITIONS | Marks the start of a section containing raw sendmail.cf commands. |
| MASQUERADE_AS | Defines the domain name used to masquerade outbound mail. |
| MASQUERADE_DOMAIN | Defines a domain that should be masqueraded. |
| MASQUERADE_DOMAIN_FILE | Identifies a file that lists domains that should be masqueraded. |
| MASQUERADE_EXCEPTION | Defines a host that should not be masqueraded. |
| MODIFY_MAILER_FLAGS | Overrides the flags for a mailer. |
| OSTYPE | Selects a file containing operating system-specific attributes. |
| RELAY_DOMAIN | Defines a domain for which mail should be relayed. |
| RELAY_DOMAIN_FILE | Identifies a file that lists domains for which mail should be relayed. |
| SITE | Identifies a locally connected UUCP host. |
| SITECONFIG | Identifies the file that lists all of the locally connected UUCP sites. |
| TRUST_AUTH_MECH | Defines a list of trusted authorization mechanisms. |
| undefine | Clears the value set for a configuration variable. |
| UUCPSMP | Maps a UUCP hostname to an Internet hostname. |
| VERSIONID | Defines version control information for the configuration. |

# Table A.1 Sendmail m4 Macros and Configuration Commands (continued)

| Command | Usage |
| --- | --- |
| VIRTUSER_DOMAIN | Defines a virtual domain that will be accepted for processing through the virtusertable. |
| VIRTUSER_DOMAIN_FILE | Identifies the file that lists virtual domains that will be accepted for processing through the virtusertable. |

The built-in m4 commands shown in Table A.1—those listed in lowercase characters—are divided between two commands used to control the flow of output and two commands used to set macro values. The two commands that control the flow of output are dnl and divert. dnl command is used at the end of a line to clean blank lines from the output or at the beginning of a line to indicate that the line is a comment. The divert(-1) command marks the end of the block of comment text and the divert(0) command accepts -1 and other numeric arguments; the values 1 to 9. (See Table 4.2 in Chapter 4, "Creating a Sendmail Configuration.") These nine values are used in sendmail m4 macros to direct data to various parts of the sendmail.cf file. But you will not use these values directly in your configuration.

A group of commands—examples of which are LOCAL_CONFIG, LOCAL_RULESET, and MAILER_DEFINITION—allows you to send data to various parts of the sendmail.cf file without using the various divert directly. Commands such as LOCAL_CONFIG and MAILER_DEFINITION mark the start of raw sendmail.cf code that should be included in some part of the output file. These commands make it possible for you to customize the sendmail.cf file in any way. See the "Local Code" section later in this appendix for a full list of these macros.

The two built-in m4 commands that set macro values are define and undefine resets a variable to its default value. More configuration parameters can be controlled through the define command than any other; correspondingly, more of this appendix is dedicated to define variables than to anything else.

Several of the macros—almost half—do essentially the same thing as the define command: they set a variable to a value. MASQUERADE_AS, MASQUADE_DOMAIN, and VIRTUSER_DOMAIN_FILE are all examples of commands used to set variables. All of these commands are covered later in this appendix.

The TRUST_AUTH_MECH macro is a section of a macro that complements a define. As you'll see the "define" section of this appendix, the parameter CONFAUTH_MECHANISMS can be used to define the trust mechanisms that your server will advertise to other servers. The TRUST_AUTH_MECH macro is the inverse of this. It identifies the mechanism that your server will accept from other servers. The same list of keywords used to configure the CONFAUTH_MECHANISMS parameter in the "define" section can be used to set TRUST_AUTH_MECHANISMS.

The macro names OSTYPE, DOMAIN, FEATURE, MAILER, HACK, and SITECONFIG are all names of subdirectories within the cf directory. The value passed to each of these macros is a name of a file within the specified directory. For example: the OSTYPE(linux) tells m4 to load the file linux from the ostype source code found. The .m4 source files pointed to by the OSTYPE, DOMAIN, FEATURE, and MAILER commands are built primarily from define and FEATURE commands.

Two of the macros that are also directory names, SITECONFIG and HACK, are rarely used. SITECONFIG points to a source file that contains SITE macros that define the UUCP connected to the local host. You create the file containing the SITE macros and then invoke it with the SITECONFIG command. These commands, along with UUCPMPT, are obsolete. The HACK macro points to a source file that contains a temporary fix to the configuration. The use of hacks is generally discouraged.

# Complete Command Reference

A.1 contains approximately forty entries. If you have experience configuring Sendmail, you might be surprised by the sheer number of commands. Sendmail, like everything else, has been suffering from "feature creep." A few years ago, configuration reached its simplest point. Then abuse of the system by spammers caused new features to be added. Some of these new features—for example, the new databases—have made old commands such as SITE, SITECONFIG, and UUCPMPT obsolete.

# define

define sets a value for a sendmail.cf macro, option, or class. Most parameter values are defined in m4 source files, not in the .mc file itself. Because many different parameters are equivalent to macros, classes, and

```
define(``confMAILER_NAME\`, ``MAILER_DAEMON\`)
```

placed in an m4 source file has the effect as MAILER_DAEMON placed directly in the sendmail.cf file. Most of the parameters default to a reasonable value and thus do not have to be explicitly set in the m4 file. The undefine command sets a variable back to its default value. For example:

```
undef(``confAUTO_REBUILD\`)
```

resets confAUTO_REBUILD to the default value even if the configuration previously set to true.

The list of define parameters shown below is quite long. The default value of each parameter is shown in the listing—unless there is no default. In the parameter description list, the name of the corresponding sendmail.cf macro, or class is shown enclosed in squares ([]). Macro names begin with a dollar sign ($j), class names begin with a dollar sign and an equal sign ($w), and options are shown with long option names (SingleThreadDelivery).
