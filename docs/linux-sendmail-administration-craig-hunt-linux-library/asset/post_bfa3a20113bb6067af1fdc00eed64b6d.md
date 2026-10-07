
sendmail.cf file. In fact, the last time I edited an Options section was years ago, before the development of the m4 macros. It was sometimes necessary back then to move a sendmail.cf from one operating system to another. In those cases, it was necessary to edit the options to fit the new environment. It is not necessary now, because the m4 macros build a sendmail.cf customized for the target operating system. The Message Precedence section that follows the Options section also requires no modifications.

# The Message Precedence Section

Message Precedence is used to assign priority to messages entering the queue. By default, mail is considered “first-class mail” and is given a precedence of 0. The higher the precedence number, the greater the precedence of the message. But don't get excited. Increasing priority is essentially meaningless. About the only thing you can select is negative precedence number, which indicates low-priority mail. Because error messages are not generated for mail with a negative precedence number, low priorities are useful for mass mailing. The precedence values from the sample sendmail.cf are shown in Listing 7.9.

- Listing 7.9 Standard Message Precedence Values

```
#############################
# Message precedences #
#############################
Pfirst-class=0
Pspecial-delivery=100
Plist=-30
Pbulk=-60
Pjunk=-100
```

The P command defines precedence. The format of the command is:

```
Pname=number
```

where P is the command. name is the text name used to request the precedence and number which is the numeric precedence value associated with the text.

To request a precedence, mail must include a Precedence header that specifies the name associated with the desired precedence. For example, to request a precedence of -30, add the following header to the mail message:

- Precedence: list

Precedence values are rarely used, and to be any of use at all, the remote user must know the precedence names. The five precedence values included in the sendmail.cf file are the standard names that are known to all other mail systems. If you add a new precedence

![](img/9639113aa446fb8976cb3d377f7aafdd_224_0.png)

value, most remote users will never know the name associated with the precedence and thus will not use it. The precedence values that come with your Linux system are not that you'll ever need.

# The Trusted Users Section

Trusted users are allowed to change the sender address when sending mail. The command defines trusted users. Its syntax is:

```
T=user
```

where T is the command and user is a valid username from the /etc/passwd file.
The trusted users defined in the sendmail.cf file that comes with your Linux system are root, uucp, and daemon. The entire Trusted Users section is shown in Listing 7.10.

- Listing 7.10 The sendmail.cf Trusted Users Section

```
############################
# Trusted users #
############################
# this is equivalent to setting class 't'
#f/etc/mail/trusted-users
Troot
Tdaemon
Tuucp
```

The T command is not the only way to define trusted users. Any user listed in class t is a trusted user. As described in Chapter 6, usernames can be added to class t with the TRUSTED_USERS parameter or the use_ct_file feature. If use_ct_file is specified, trusted users are read from the /etc/mail/trusted-users file. In this configuration, the use_ct_file feature was not used. If it had been used, the T commands in Listing 7.10 would not be commented out.

> NOTE Do not modify the Trusted Users list. Allowing users to send mail using another user's name is a potential security problem.

# The Format of Headers Section

The Format of Headers section defines the headers that Sendmail inserts into mail. Headers are defined by H command. The header definitions from sendmail.cf file are shown in Listing 7.11.

**Listing 7.11 Header Formats in sendmail.cf**

```
############################
# Format of headers #
############################
HReturn-Path: <$g>
HReceived: $s from $s
HAuth_type: $(auth_type) bits
HTls_version: $(tls_version) bits
HDate: $a
HDate: $a
HFent-From: $x <g>
HFrom: $x <g>
HFull-Name: $x
HPost-Date: $a
HReceived-Date: $b
HMessage-Id: $t.$i
```

Each line begins with H command, which optionally followed by header flags enclosed in marks. The header flags control whether the header is inserted into mail for a specific mailer. If no flags are specified, the header is used for all mailers. If a flag is specified, the header is used only for a mailer that has the same flag. (Mailer definitions are covered later.) Each line also contains a header name and a header template. These fields define the structure of the actual header. Macros in the header template are expanded before the header is inserted in message. The first header in Listing 7.11 contains $g, which tells Sendmail to use the value stored in g macro. g macro holds the sender's email address. Assume that the sender is, the header might contain:

```
Return-Path: <david@sendmail.com>
```

The headers in Listing 7.11 provide examples of using the conditional syntax in header templates. The conditional syntax is an if/else construct: ? is "if," | is "else," and ; is "endif." This is exactly the same conditional syntax that was described for D command, and it is used in the same way. An example from Listing 7.11 is:

```
H?F-From: $x <g>|
```

H is the command. ?F is a flag value. From: is the header name, and ?x is the template, which uses conditional syntax. This conditional template says that if (?) exists, use <g> as the header template, else use as the template. The macro contains the full name of the sender. Thus, if it exists, the header is:

From: david@sendmail.org

If x doesn't exist, the header is:

From: david@sendmail.org

The headers provided in the Linux sendmail.cf are sufficient for a basic installation. You'll see additional header declarations in Chapter 11, "Stopping Spam," for mail filtering, but the basic declarations shown in Listing 7.11 will be found on all systems.

All five sections discussed so far—Local Info, Options, Message Precedence, Trusted Users and Format of Headers—define configuration values used by Sendmail. These sections are essentially passive, telling Sendmail things such as the structure of headers or the locations of files. These sections have not defined the actions that Sendmail should take. With changes with the next section. The Rewrite Rules section contains the instructions that Sendmail uses to process mail.

# Rewrite Rules Section

The Rewrite Rules defines the rules used to parse e-mail addresses from user mail programs and rewrite them into the form required by the mail delivery programs. Rewrite rules match the input address against a pattern, and if a match is found, rewrite the address in a new format using the rules defined in the command. The format of a rewrite rule is:

```
Rpattern template
```

where R is the command. pattern selects the address to be modified and template rewrites the address.

# The Mailer Definitions Section

Rewrite rules divide e-mail addresses into tokens for processing. Tokens are strings of characters delimited by operators defined in the OperatorChars option, and the operators themselves. The left-hand side of a rewrite rule contains a pattern defined by macro variables and literal values and special symbols. The tokens from the input address are matched against the pattern. If the address matches the pattern, the address is rewritten using the template defined in the right-hand side of the rewrite rule. The template is also defined with literals, macro values, and special symbols.

A rewrite rule may process the address several times because, after being rewritten, the address is again compared against the pattern. If it still matches, it is rewritten again. The cycle of pattern matching and rewriting continues until the address no longer matches the pattern. No further processing is done by this rewrite rule, and the address is passed to the next rule in line.

Individual rewrite rules are grouped together in rulesets that related rewrite rules can be referenced by a single name or number. The S command marks the beginning of a ruleset and identifies it with a name and optionally a number. Therefore, the command Sfinal=4 marks the beginning of the ruleset known as either final or 4, and SLocal_check_mail marks the beginning of the Local_check_mail ruleset.

> NOTE Prior to Sendmail.81, many rulesets were known only by numbers and did not have associated names.

Rewrite rules are the heart of the sendmail.cf file and they make up the bulk of the command lines in the configuration file. The sample sendmail.cf we have been examining in this chapter contains more than 425 rewrite rules.

The Mailer Definitions section defines the instructions used by Sendmail to invoke the mail delivery programs. Mailer definitions begin with the mail command (M). Searching through the Mailer Definitions section of the sample sendmail.cf configuration file for lines that begin with M produces the mailer definitions list shown in Listing 7.12.
