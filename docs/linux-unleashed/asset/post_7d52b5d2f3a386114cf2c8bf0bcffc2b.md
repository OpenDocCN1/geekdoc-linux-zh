
The local mails used by **sendmail** is defined in the line that contains the variable **LOCAL_MAILER_DEF** and looks like this:

```
define(LOCAL_MAILER_DEF, mailers.linux)dnl
```

This line is necessary because **sendmail** doesn’t actually handle mail delivery. Instead, another program takes care of this step. By default, the value used for the local mailer (which is almost always *deliver*) is contained in a file called *mailers.linux*. This file is referenced in the **LOCAL_MAILER_DEF** entry in the *sendmail.m4* file. This requires you to check the *mailers.linux* file in the same subdirectory (usually */usr/local/lib/mail*) to ensure the *deliver* program (or whatever delivery agent you use) is properly entered. A typical *mailers.linux* file looks like this:

```
# mailers.linux
Mlocal, P=/usr/bin/deliver, F=$1sm$DMP, S=10, R=25/10, A=deliver $u Mprog, P=/bin/sh, F=1sDFMeuP, S=10, A=sh -c $u
```

The *deliver* mail delivery agent is also specified in the file *Sendmail.mc*, which is used to build *sendmail.cf*. You need to check this *Sendmail.mc* file, too, if the name of your delivery agent is not *deliver*. (If you are using *deliver*, don’t worry about this file.) The *Sendmail.mc* file is important and must be read in when *sendmail.m4* is processed. There is usually a line in *sendmail.m4* that makes sure this happens. The line, which usually occurs at the top of the *sendmail.m4* file, looks like this:

```
include(Sendmail.mc)dnl
```

You may need to specify some entries in the **PSEUDODOMAINS** variable. This variable is used to handle systems that can’t expand into domain names properly, usually UUCP networks. The entries in the **PSEUDODOMAINS** field tells *sendmail+IDA* not to use DNS for these networks (which will always fail). Typically, the **PSEUDODOMAINS** variable is set to the following values:

```
define(PSEUDODOMAINS, BITNET UUCP)dnl
```

You can use the **PSEUDONYMS** field to hide your machine names from the outside world. This means that whether mail was sent from *merlin.tpci.com* or *chatten.tpci.com* doesn’t matter: the recipient on another network sees only the address *tpci.com*. This is called “*hiding*” the local machines. When used, *sendmail* accepts mail from all machines identified in the **PSEUDONYMS** variable. The **PSEUDONYMS** field is usually used as shown in the following line:

```
define(PSEUDONYMS, tpci.com)dnl
```

This entry lets any machine with the network type *tpci.com* send mail through *sendmail*.

To define the name of your local machine, you use the DEFAULT_HOST variable. This is usually defined as the same name as your mail server (or your basic machine's name if you are not on a network). For example, the following entry can be used to set the default mail server's name:

```
define(DEFAULT_HOST, merlin.tpci.com)dnl
```

If you do not set a valid name for the DEFAULT_HOST variable, no mail will be returned properly to your system.

If your system is not a mail gateway to the Internet (or other networks that are accessible from your LAN), you can set your Linux system to send mail on to another machine for processing. This is done by setting the RELAY_HOST and RELAY_MAILER variables in sendmail.m4. These variables set the name of the mail server that all mail should be passed on to. For example, to set your local system to route all outbound mail to a machine called wizard, set these two lines to look like this:

```
define(RELAY_HOST, wizard)dnl
define(RELAY_MAILER, UUCP=A)dnl
```

The RELAY_MAILER line specifies the mailer to use to send messages on to the RELAY_HOST.

## Configuration Table Locations

There are several lines in the sendmail.m4 file that define configuration tables. For the most part, these configuration files are under the directory defined by LIBDIR. This section of the sendmail.m4 file has several lines that look like

```
define(ALIASES, LIBDIR/aliases)dnl
define(DOMAINTABLE, LIBDIR/domaintbl)dnl
```

and so on for about seven configuration file definitions in total. You can change any of these values if you want, but be sure to move the files themselves to the specified location. On the whole, it is best to leave the files in their default location.

The file decnetxttable is used to translate domain names into DECnet style names. This is a holdover from earlier versions of sendmail and will probably never be necessary for Linux users (unless your Linux machine is on a DECnet system).

The domaintable file is used to force sendmail to perform specific instructions after using DNS. The file, which is almost never used on Linux systems, allows you to provide expansion of short-form names. For example, suppose you often send mail to the host reallylongname.reallybignet.com but don't want to type that entry each time. You can place an entry in the domaintable file that looks like

```
reallylongname.reallybignet.com        big.com
```

so that whenever you send mail to bill@big.com it is expanded by sendmail to bill@reallylongname.reallybignet.com. The domain table file can also be used to correct common typographic mistakes. For example, if you find many users sending mail to abcdef.com instead of abcdefe.com, you can add a line to the domain table file that corrects the domain name. Such a line looks like this:

```
abcdef.com        abcdefe.com
```

The format of the file is always correct domain followed by the incorrect (or shortened) domain name.

The *genericfrom table* is used to hide local usernames and machine addresses by converting local usernames to a generic ID that has no obvious connection to the username. It is seldom used by Linux systems because the general convention is to use real names on email and similar data. The companion file, *xaliases*, performs the generic to real conversion when mail comes back from the outside world.

The *mailertable* table is used to define any special handling for hosts or domains. Most often, *mailertable* is used to specify how certain domains or hosts are accessed and which protocol to use for them. This file doesn't have to be modified if your system only uses UUCP, but if you use SMTP or DNS, you should verify its contents.

The *mailertable* file is read from the first line down, and *sendmail* processes mail based on each line in the file. For this reason, place the most specific rules at the top of the file, with more general rules after. Rules are specified in a format that gives the method of connection, then the remote system or domain. The syntax is

```
mailer delimiter relayname     remote
```

where *mailer* is the transport to use, *delimiter* is a special character, *relayname* is the name of the system to pass the mail to, and *remote* is the remote host or domain name. The *mailer* can be one of the following values:

- **TCP-A**	TCP with Internet-style addresses
- **TCP-U**	TCP with UUCP-style addresses
- **UUCP-A**	UUCP with Internet-style addresses

The *delimiter* has a special meaning and must be one of the following characters:

- **!**	strips the hostname from the address before forwarding
- **,**	doesn't modify the address at all
- **:**	removes the hostname only if there are intermediate hosts specified

The mailertable rules can be built quite easily when you are forwarding mail to a remote mail server. For example, to force sendmail to use UUCP through a remote mail server called wizard to connect to the remote system roy.sailing.org, add a rule like this to the mailertable file:

```
UUCP-A,wizard   roy.sailing.org
```

On a more general level, you can have a rule like this one

```
TCP-A,wizard    chatton.com
```

which forwards any mail destined for the remote network chatton.com to the local mail server wizard via TCP.

The pathtable table is used to define explicit routing to remote hosts and networks. The format of each line in the pathtable file uses a syntax similar to a UUCP path alias, with entries appearing alphabetically in the file. The use of the pathtable file is rare because most Linux systems can handle the routing without explicit instructions.

The uucprelays file is used to short-circuit the UUCP path to a remote site when there is a better path. For example, if your users often use the path wizard!bignet!merlin!tcpy and you create a direct link to tcpi, you can use uucprelays to redirect the mail. This file is seldom used by Linux system users.

The uucpxtable file is used when a UUCP-style address must be used for mail delivery. The file provides the instructions for converting a DNS format address to a UUCP format address. If you are using a mail server other than your current machine or want to use UUCP to connect to specific machines because of reliability factors, this table is necessary.

This file contains a number of entries that has a format that gives the UUCP style name followed by the domain name, such as this one:

```
chatton       chatton.com
```

This tells sendmail that any mail for chatton.com should be rerouted via UUCP to chatton (UUCP-style addressing). This forces mail addresses to let's say, yvonne@chatton.com to be rewritten as chatton!yvonne, which can be handled by UUCP.

## Building sendmail.cf from sendmail.m4

Now that you have configured the sendmail.m4 file and its dependent files, you can generate the sendmail.cf file. This is done with the m4 processor. When the sendmail.m4 file is ready to be processed, issue the command

```
make sendmail.cf
```
