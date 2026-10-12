PART Ⅱ

# TABLE 10.1 *sendmail.cf Command Characters*

| Command Character | Command Syntax and Example | Function |
|---|---|---|
| | | |
| `#` | `#` comments are ignored | A comment line. Always use lots of comments. |
| `#` | `# Standard RFC822 parsing` | |
| `D` | `DX string` | Defines a macro `x` to have the string value `string`. |
| `D` | `DMmailhub.gonz o.gov` | |
| `D` | `D({MacroName})value` | Defines long macro `{MacroName}` to have the value, `value`, then referenced later with `\$({MacroName})`. |
| `C` | `D(Relay)mailhub.gonz o.gov` | |
| `C` | `CX word1, word2, and so on` | Defines a class `X` as `word1`, `word2`, and so on. |
| `F` | `CWlocalhost myusername` | |
| `F` | `FX/path/to/a/file` | Defines a class `X` by reading it from a file. |
| `H` | `Fw/etc/mail/host_aliases` | |
| `H` | `H?mailerflag?name::template` | Defines a mail header. |
| `H` | `H?F?From: $q` | |
| `O` | `OX option arguments` | Sets option `X`. Most command-line options can be set in *sendmail.cf*. |
| `O` | `OL9 # sets the log level to 9.` | |
| `P` | `Pclass=nn` | Sets mail delivery precedence based on the class of the mail. |
| `P` | `Pjunk=100` | |
| `V` | `Vn` | Tells V.8 *sendmail* the version level of the configuration file. |
| `V` | `V3` | |
| `K` | `Knane class arguments` | Defines a key file (database map). |
| `M` | `Kuucphosts hash /etc/mail/uucphosts` | |
| `M` | `Mname,field_1=value_1, ...,` | Defines a mailer. |
| `M` | `Mprog,P=/bin/sh,F=1sD, @A@sh -c $u` | |