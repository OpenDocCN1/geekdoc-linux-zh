pop This mailer supports the Post Protocol. On Linux systems, POP mail is provided by a specialized POP mail daemon, so the MAILER(pop) command is not needed or used.

procmail This mailer provides a procmail interface for the mailtable. Even though procmail is used as the Linux local mail, the MAILER(procmail) command is not required. See the discussion of procmail in Chapter 11.

mail111 This is an obsolete mailer that was used only on DECnet mail networks that used the mail111 mailer.

phquery This mailer provides CSO phone book (ph) directory service using the phquery program. User directory services are usually configured in the user agent mail, not in Sendai.

cyrus This mailer provides a local mail delivery program that uses a mailbox architecture. This architecture permits the use of user+detail address syntax where detail is interpreted as a mailbox name. Despite some advanced features, cyrus and cyussbb are not widely used.

qpage This mailer provides an interface from e-mail to pagers using the QuickPage program.

Not everything about mailers is defined in the source files loaded by the MAILER macros. We have already seen that many define commands relating to mailers are specified in the OSTYPE source file. Additionally, you can define your own owners or override mailer parameters using macro commands that let you put raw sendmail.cf code directly into an m4 source file.

# Local Code

There are several m4 macros that allow you to directly modify the sendmail.cf file with unadulterated sendmail.cf configuration commands. These macros are placed at the beginning of a block of sendmail.cf code and tell them m4 where to put code in the output file. These macros are:

LOCAL_RULE LOCAL_RULE_n heads a section of code to be added to ruleset n, where n is 0, 1, 2, or 3. The code follows the LOCAL_RULE command is sendmail.cf cf rewrite rules.

LOCAL_CONFIG LOCAL_CONFIG has a section of code to be added to the sendmail.cf file after the local information section and before the rewrite rules. The section of code contains standard sendmail.cf configuration commands.

LOCAL_RULESETS This macro heads a section of code that contains a complete ruleset that is be added to the sendmail.cf file. Generally, these are named as opposed to numbered rulesets.