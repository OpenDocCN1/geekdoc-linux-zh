used. Lines beginning with the hash symbol (#) are comment lines and the commands continue to the end of the line.

Table 16.2 outlines the main `sendmail.cf` configuration command characters.

**TABLE 16.2 — `sendmail.cf` CONFIGURATION COMMAND CHARACTERS**

| Command Character | Description | Example/Meaning |
|---|---|---|
| `#` | A comment line | Comment lines are ignored |
| space | Continue the previous line |  |
| Tab | Continue the previous line |  |
| C | Define a class macro | `C0 @ % \` defines class 0 as the list of characters @, %, and ! |
| D | Define a macro | For example, `D$host.some.domain` defines `s` as `some.host.domain` |
| F | Define a class macro from a file or pipe | `Fw/etc/sendmail.cw` indicates that the value of `s` is read from the file `/etc/sendmail.cw` |
| H | Define a header | `H?P?Return-Path: <$g>` |
| K | Create a keyed map entry | `Kaccess hash -o /etc/mail/access` defines the access list database |
| M | Define a mail delivery agent | `Mprocmail` defines the program `procmail` as a mail delivery agent |
| O | Define an option | For example, `OAliasFile=/etc/aliases` defines the location of the aliases file |
| P | Define delivery priorities | `Pfirst-class=0` indicates that the name first-class is given the number 0 |
| R | Define a rule |  |
| S | Declare start of a rule-set | `$0` declares the start of rule-set 0 |
| T | Declare trusted users | `Troot` defines root as a trusted user |
| V | Version number of the configuration file | `V8/Berkeley` defines the configuration file version as V8/Berkeley |

# ## DEFINING CLASS COMMANDS

Two commands define classes: C and F. A class defines an array of values. When multiple values are handled in the same way, a class definition can be used. Classes allow sendmail to compare against a list of values instead of a single value.