
Because the sendmail.cf file is designed to be read and parsed quickly and efficiently by sendmail, it uses a format and syntax which is far from easy for humans to read. By way of example, consider the following extracts from a sendmail.cf:

```
H?P?Return-Path: <$g$>
HReceived: $p$rom $s $?$_($$ $from $.$_)
        $.by $; (y/sz? $7? with $r$, id $i$u)
            for $u; $i;
            $. $b
H?D?Resent-Date: $a
H?D?Date: $a
H?F?Resent-From: $x$x <$g>$ $a$.
H?F?From: $x$x <$g$>$!$g$.
H?x?Full-Name: $w
# HPosted-Date: $a
# H?I?Received-Date: $b
H?M?Resent-Message-Id: <$t.$i$e$>
H?M?Message-Id: <$t.$i$e$>
```

> **Note**
> 
> This sample from the sendmail.cf file illustrates a more cryptic section of the file. Some parts of the file are easier to read for humans, but generally the file is obscure, as this example illustrates.

Even though the file is hard to read, the contents of the sendmail.cf file control the behavior of sendmail. The file provides several key pieces of information to sendmail including the following:

- The location of files and directories sendmail needs to use during regular operation
- The definitions that sendmail uses when rewriting addresses
- The mail header lines sendmail should modify, or pass through when it routes a message
- The sets of rules sendmail should use to select the appropriate delivery agent
- The definitions of mailer delivery agents

## GENERAL STRUCTURE OF THE sendmail.cf FILE

Luckily, it is not necessary to write a sendmail.cf file from scratch. Generally, you can use the default sendmail.cf file that comes with your sendmail distribution and then modify it to suit the needs of your site. The structure of the file will remain generally unchanged and you will only need to edit specific entries.

Unfortunately, this is still not a trivial task. The sendmail.cf configuration commands use a terse syntax and command set and are difficult to remember or remain fluent in. Each configuration command consists of a single letter starting at the beginning of a line. The single command character is followed by other information pertinent to the command being used. Lines beginning with the hash symbol (#) are comment lines and the commands continue to the end of the line.

Table 16.2 outlines the main `sendmail.cf` configuration command characters.

**TABLE 16.2 — `sendmail.cf` CONFIGURATION COMMAND CHARACTERS**

| Command Character | Description | Example/Meaning |
|---|---|---|
| `#` | A comment line | Comment lines are ignored |
| space | Continue the previous line |  |
| Tab | Continue the previous line |  |
| C | Define a class macro | `C0 @ % !` defines class 0 as the list of characters @, %, and ! |
| D | Define a macro | For example, `D$host.some.domain` defines `s` as `some.host.domain` |
| F | Define a class macro from a file or pipe | `Fw/etc/sendmail.cw` indicates that the value of `w` is read from the file `/etc/sendmail.cw` |
| H | Define a header | `H?P?Return-Path: <$g>` |
| K | Create a keyed map entry | `Kaccess hash -o /etc/mail/access` defines the access list database |
| M | Define a mail delivery agent | `Mprocmail` defines the program `procmail` as a mail delivery agent |
| O | Define an option | For example, `OAliasFile=/etc/aliases` defines the location of the aliases file |
| P | Define delivery priorities | `Pfirst-class=0` indicates that the name first-class is given the number 0 |
| R | Define a rule |  |
| S | Declare start of a rule-set | `S0` declares the start of rule-set 0 |
| T | Declare trusted users | `Troot` defines root as a trusted user |
| V | Version number of the configuration file | `V8/Berkeley` defines the configuration file version as V8/Berkeley |

### DEFINING CLASS COMMANDS

Two commands define classes: C and F. A class defines an array of values. When multiple values are handled in the same way, a class definition can be used. Classes allow sendmail to compare against a list of values instead of a single value.

For example to assign the values bwc and dmz to the class you can use the following:

```
Cw bwc dmz
```

A class can also be defined specifying list values in multiple lines:

```
Cw bwc
Cw dmz
```

Class values can be loaded from a file by using the F command. For example to read the values for a class w from a file you can use the following:

```
Fw/etc/sendmail.cw
```

The file /etc/sendmail.cw should contain all the strings that you want to assign to class w. For instance, to assign the values bwc and dmz to class w using the /etc/sendmail.cw file, it should contain these values, one per line as follows:

```
bwc
dmz
```

### Defining Macro Command

The D command defines a macro and stores a value in it. When the value is defined it can be used by other commands in the sendmail.cf file. This makes it possible to share the same configuration file among different systems. The only changes needed are to define a few system-specific macros.

User-defined macros use uppercase letters. Lowercase macro names are reserved for internal use by sendmail. If a macro called x is defined, its value can be retrieved later using `$x`. The following are some example macro definitions:

```
Dwphoenix
DDbwc.org
Dj$w.$D
```

Here we have one user-defined macro and two system macros. The lowercase letter w is a system macro reserved for hostname. We have defined w as phoenix in this example. The letter D is a user-defined macro for the domain name. We have defined D as bwc.org. The sendmail system macro definition `Dj$w.$D` defines the macro j as `$w.$D`. The lowercase letter j is a system macro reserved for the domain name of a site. After we expand the values of the macros `$w` and `$D`, the final value of j becomes phoenix.bwc.org.

### Defining Header Command

Mail header formats are defined with the H command. Generally the header format definitions that come with the standard sendmail.cf file need no tweaking. The standard headers are listed here:

```
H?P?Return-Path: <$g>
HReceived: $?{from} $s $?{_($s?from $._)
    $.by $j ($?/$? $d) with $i; $i?$u
    for $u; $i;
    $.$b
H?D?Resent-Date: $a
H?D?Date: $a
H?F?Resent-From: $x?$x <$g$;|$g$.
H?F?From: $?x$ <$g$>
H?X?Full-Name: $x
H?M?Resent-Message-Id: <$t.$i@$j>
H?M?Message-Id: <$t.$i@$j>
```

The syntax of the header command is the letter H, followed by an optional flag enclosed between two question marks, the name of the header, a colon, and the header template. The header template consists of literals and macros. The macros are expanded before the header is inserted into a message.

The header flags control whether the header is inserted into mail bound for a specific mailer. The flag definitions in the above example are as follows:

- **P:** Use when the mailer requires a `Return-Path` line.
- **D:** Use when the mailer requires a `Date:` header line.
- **F:** Use when the mailer requires a `From:` header line.
- **X:** Use when the mailer requires a `Full-Name:` header line.
- **M:** Use when the mailer requires a `Message-Id:` header line.

For a complete list of mailer flags refer to the “Sendmail Installation and Operations Guide.” This document is available with the standard Linux distribution as a postscript file `/usr/doc/sendmail/ops.ps`. It can also be downloaded from `http://www.sendmail.org`.

### DEFINING KEYED MAP ENTRIES

The use of external keyed databases was introduced in Version 8 of sendmail. An external keyed database can provide certain information such as a list of UUCP hosts for faster access. Keyed databases come in several forms, such as hash table or dbm formatted files. Pointers to the keyed maps are done with the `K` command in the `sendmail.cf` file.

For instance, the following command indicates that the hash table file `/etc/mail/uucphosts` contains a list of UUCP hosts:

```
Kuucp hash /etc/mail/uucphosts
```

Other typical applications of the K command are using the access database to control spam:

```
Kaccess hash -o /etc/mail/access
```

or to provide virtual user lists:

```
Kvirtuser hash -o /etc/mail/virtusertable
```

### DEFINING MAIL DELIVERY PROGRAMS

Mail delivery programs are defined using the M command in the `sendmail.cf` file. The following is the syntax of this command:

```
M<program>, <field1>=<value1>, <field2>=<value2>, etc.
```
