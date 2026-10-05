kathy@grebe.foobirds would process the address through canonify and parse.
Listing 10.8 shows an example of using canonify and parse to process an address.

# 10.8 Processing an Address through a Ruleset

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 3,parse@bird.org
canonify        input: al @ bird . org
canonify2       input: al < @ bird . org >
canonify2       returns: al < @ bird . org >
canonify        returns: al < @ bird . org >
parse           input: al < @ bird . org >
Parse0          returns: al < @ bird . org >
ParseLocal     input: al < @ bird . org >
ParseLocal     returns: al < @ bird . org >
Parse1          input: al < @ bird . org >
Mailertable     input: < bird . org al < @ bird . org >
Mailertable     input: < > org al @ bird . org >
Mailertable     returns: al < @ bird . org >
Mailertable     returns: al < @ bird . org >
MailerTriple returns: < > al < @ bird . org >
MailerTriple returns: $ # esmtp @ bird . org >
               $: al < @ bird . org >
Parse1
parse           returns: $ # esmtp @ bird . org >
               $: al < @ bird . org >
> /quit
```

Listing 10.8 processes the address @bird.org through ruleset 3, the canonify ruleset, and ruleset parse. This example shows that a ruleset can be identified by its name or number, if it has a number. All of the other rules, canonify2, Parse1, etc., that are shown in the example are called from either ruleset 3 or ruleset parse. (To find more about what these individual rules do, see the description of the rulesets in Chapter 8.)

This type of test is generally used to observe the effect of a single rule on ruleset. A realistic example would be to process various local addresses through ruleset localaddr (ruleset 5) to observe the effect that defining MAIL_HUB has on the configuration. Multi-step tests that mimic basic Sendmail processing can be more easily accomplished with some other test command.