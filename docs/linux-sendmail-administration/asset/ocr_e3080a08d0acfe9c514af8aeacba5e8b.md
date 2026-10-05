# Writing Local Rules

# Listing 9.6 A LOCAL_CONFIG Example

```
LOCAL_CONFIG
### Store a host name in variable A
DNs.foobirds.org
### Define a special NIS database
Knishosts nis -m hostnoshists is a private database
```

Listing 9.6 assumes that A is a private variable and noshists is a private database. The LOCAL_CONFIG example in Listing 9.6 is contrived, but it shows the format used by all of the macros covered in this section. Each macro is a keyword that marks the start of a variable-length block of text. The block of text ends when the next m4 macro encountered. The variation from the macros covered in this section is that each one inserts the text into a different part of sendmail.cf file.

The MAILER_DEFINITIONS macro is used to define a variable and add it to the Mailer Definitions section of sendmail.cf file. The mailer is defined using the M command described in Chapter 7. If any special rules are required by the new mailer, they are also defined in the text that follows the MAILER_DEFINITIONS macro.

Rewrite rules, and even rules, can be added to the Rewriting Rules section of the sendmail.cf file. The first line following the LOCAL_RULESETS macro is a sendmail.cf S command that defines the name of the new rule. This is followed by rewrite rules that make up the rule. Most often LOCAL_RULESETS are used for spam filtering or security. We cover the LOCAL_RULESETS macro in Chapter 11, “Stopping Spam.

To add individual rules to rules 0, 1, 2, or 3, use the LOCAL_RULE_n macro. The n in the name of this macro is the number of rules to which the rule should be added. Listing 9.7 shows rules being added to rules 1, which is also called the sender rules.

# Listing 9.7 Creating and Testing Additions to Rules 1

```
[root]# ..domain/old-foobirds.m4 ..domain/foobirds.m4
8a9
> MASQUADE_AS(`foobirds.org`).dnl
9all,13
> FEATURE(`stable`)dnl
> LOCAL_RULE_1
> R- < $w .$: $: generics $1 $) < $ $2 .
[root]# m4 ..cf/cf.m4 redhat811.mc > local-rule.cf
[root]# sendmail -bt -C local-rule.cf
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
```