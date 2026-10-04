# 660 Installing the Mail Server

Table 4-1 summarizes the one-letter control operators used in sendmail.cf. Each entry also shows an example of that operator. This table helps you understand some of the lines in sendmail.cf.

| Operator | Description |
| --- | --- |
| C | Defines a class; a variable (think of it as a set) that can contain several values. For example, Cwllocalhost adds the name localhost as the class w. |
| D | Defines a macro, a name associated with a single value. For example, DrMailer-DAEMON defines the macro n MAILER-DAEMON. |
| F | Defines a class that's been read from a file. For example, /etc/local-host-names reads the names of hosts from the file /etc/local-host-names adds them to the class w. |
| H | Defines the format of header lines that sendmail inserts into a message. For example, H?Return-Path:<sg> defines the Return-Path: field of the header. |
| K | Defines a map (a key-value pair database). For example, Karith defines the map named as the compiled-in of the same name. |
| M | Specifies a mailer. The following lines define the procmailer: Procmail=/usr/bin/procmail/DFMSphnu9,SerF romSMTP/HFromSMTP,REnvToSMTP/HDrSMTP,T-DN S/RFC22/HDrUnX,Aprocmail -Y -m $f su. |
| 0 | Assigns a value to an option. For example, 0 AliasFile=/etc/aliases defines the AliasFile to /etc/aliases, which is the name of the sendmail alias file. |
| P | Defines values for the precedence field. For example, Pjunk-100 sets to -100 the precedence of messages marked with the header field Presence: junk. |
| R | Defines a rule (has a left-hand side and a right-hand side; if input matches the left side, the right-hand side replaces it - this rule is called rewriting). For example, the rewriting R$: $1 strips semicolons. |
| S | Labels a ruleset you start defining subsequent R controls. For example, Canonify=3 labels the ruleset as canonify or rules3. |
| T | Adds a username to the trusted class (class t). For example, Troot adds root to the class of trusted users |
| V | Defines the major version number of the configuration file. For example, V10/Berkeley defines the version number as 10. |