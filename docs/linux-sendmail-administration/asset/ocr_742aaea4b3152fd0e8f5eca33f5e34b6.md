The second command in Listing 2.1 is slightly different. It evaluates the delivery address craig. Because the address has no hostname part—i.e., no at-sign (@) followed by a host or domain name—the address is assumed to be the name of a user on the local system. Sendmail checks whether the username is deliverable on the local host. The host value is not provided as part of the delivery triple for local mail delivery because no remote host is involved. The internal mailer for local delivery is local, and in Listing 2.1 the user value that would be passed to the local mailer is craig.

# Formatting E-Mail Addresses

Once Sendmail selects a mailer, it must properly format the mail for that mailer. Sendmail uses commands called rewrite rules to transform the e-mail address received from the MUA into the format required by the MTA. The bulk of the Sendmail configuration file is composed of rewrite rules. These are individual lines that define a pattern and a transformation. If the input address the pattern defined in a rule, it is rewritten using the transformation defined in that rule.

Rules are grouped together into rulessets, which are internally identified by a name or a number. Rulesets can be called like functions from individual rewrite rules to process complex addresses. Certain rulesets are assigned special by Sendmail and are used to process different types of addresses. For example, delivery addresses are processed by the canonify ruleset (also known as ruleset 3), which processes all addresses to put them into the format expected by Sendmail, and by the parse ruleset (also known as ruleset 0), which creates the delivery pipeline.

You can watch the rulesets in action by running the sendmail command with the -bt option - replaces delivery in test mode. Once it is in test mode, it will accept a list of rulesets and an address to process through those rulesets. In Listing 2.2, the sendmail command is run with the -bt argument and asked to process ed@xy.com through canonify and parse.

# Listing 2.2 Watching Rewrite Rules in Action

```
[craig]$ sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter<ruleset>,parse ed@xy.com
canonify       input: ed < @xyz com
canonify2      input: ed < @xyz com >
Canonify2     returns: ed < @xyz com>
canonify      returns: ed < @xyz com>
parse         input: ed < @xyz com>
Parse0        input: ed < @xyz com >
```