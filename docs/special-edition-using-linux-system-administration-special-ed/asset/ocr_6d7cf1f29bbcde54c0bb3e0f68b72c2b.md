# Defining Mail Priority

Each message entering the mail queue is assigned a priority by sendmail. The P command in the `sendmail.cf` file defines the priority values available to users. By default, messages receive a priority of 0 unless otherwise indicated. Negative priority values lower message priorities, and positive values raise message priorities.

> > **Tip**  
> > In addition to being lower on the priority scale, messages with negative priority values do not generate error messages. This means negative priority values can be useful for bulk mailing lists that are likely to generate large numbers of mail messages.

The default `sendmail.cf` file includes the following priority definitions:

```
Pfirst-class=0
Pspecial-delivery=100
Plist=-30
Pbulk=-60
Pjunk=-100
```

# Defining Rules and Rule Sets

In this section we will take a brief look at address rewriting concepts. A detailed discussion of this topic is beyond the scope of this book. For a complete discussion of this topic refer to *sendmail* by Brian Costales and Eric Allman, published by O'Reilly.

Rules and rule sets make more sense when they are looked at together. Address rewriting rules are defined by the R command. Rule sets are defined by the S command. A rule set may contain zero or more individual rules. The following shows the syntax of the R and S commands:

```
$0
R<left side>    <right side>    <comment>
```

The line `$0` marks the start of rule set 0. The next line starting with `R` defines a rule.

The fields in a rule must be separated by one or more tab characters and not by white spaces. White spaces can be used inside a field. The comment field is ignored.

The syntax of rules is extremely cryptic. Therefore if you do not write good comments when you write a rule, it can be very difficult to determine the purpose of the rule at a later date.

We will use the abbreviated terms LHS (left-hand-side), and RHS (right-hand-side) to describe the syntax. The input address is applied to the pattern on the left-hand-side. If the left-hand-side evaluates to true, then the right-hand-side is executed. If LHS evaluates false, then that rule is skipped and it moves on to the next rule in the set.

**The Left-Hand-Side Pattern**  
The left-hand-side pattern consists of normal words and meta-symbols. Normal words are matched directly. Meta-symbols are specified using a dollar sign. Table 16.3 outlines the meta symbols used in the LHS of rules.