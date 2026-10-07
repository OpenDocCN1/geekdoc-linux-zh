
rule. At first glance, one might think that flow control is not required for rule because it is the last rule in the ruleset and will end after that rule executes. On closer examination the problem is clear: the third rule will never finish executing because it is an infinite loop. The $* pattern matches zero or more tokens, it will match anything, the string Wrong format. Thus, the pattern will match the output of the rule. Because the rule recursively processes its own output against the pattern $*, which matches anything, a loop will ensue. Sendmail detects loops and complains when one is found, as shown in Listing 8.6.

# Listing 8.6 Results of a Tight Loop in the Sendmail Configuration

```
[root]# sendmail -bt -Ctest.cf
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enterter <ruleset> <address>
 >=ClassTest
R$* @ $~w $@$ Found it
R$* @ $^w $@$ Not in class w
R$* 
    Wrong format
> ClassTest input: craig
ClassTest
Infinite loop in ruleset ClassTest, rule 3
ClassTest
returns: Wrong format
> ^D
```

In Listing 8.6, sendmail is again run with the -bt argument. The =S command, described in Chapter 10 with other test commands, is used to display the contents of the ruleset ClassTest. In this example, the template in the third rule of the ruleset does not start with $. In this case, when ClassTest runs with an input address of craig, an infinite loop ensues. Sendmail displays an error message stating that an infinite loop was encountered and exactly where the loop occurred.

Loops do not need to be as tight as the one shown in Listing 8.6. A loop can involve multiple rules because a ruleset can be called by a rule using the $name syntax. The called rule finishes processing, it returns a rewritten address to the calling rule. The returned e-mail address is then compared against the pattern in the calling rule. If it still matches, the ruleset is called again. Use $: and $$ to prevent loops whenever they can occur.

# Rewrite Rules 237

The $>name symbol calls ruleset name and passes the address defined by the remainder of the template to that ruleset for processing. For example, both rules in the ruleset named CallRulesets, shown below, call other rulesets:

```
CallRulesets
R$* @-            $: $: canonify $1 @ $2
R$* @-            $: final $1
```

The template in the first rule calls ruleset canonify ($canonify), and passes the contents of $1, a literal @, and the contents of $2. The template starts with the $: symbol, so the first rule executes only once when the pattern matches. The template in the second rule calls ruleset final ($final) and passes the contents of $1 (Because the pattern in the second ruleset includes only one symbol, $1 contains the entire input address.) The second rule will also execute once because its template starts with $: Listing 8.7 shows the CallRulesets ruleset in action.

# Listing 8.7 Calling Another Ruleset from a Rule

```
[root] sendmail -bt -Ctest.cx
ADDRESS TEST MODE (ruleset 3 NOT AUTOMATICALLY INVOKED)
Enter<ruleset> <address>
> CallRulesets julie@red
CallRulesets      input: julie @ broadest
canonify          input: julie @ broadest
canonify2         input: julie < @ broadest
canonify2         returns: julie < robin foobirds .org >
canonify          returns: julie . robin foobirds .org >
final             input: julie < robin foobirds .org >
final             returns: julie . robin foobirds .org
CallRulesets      returns: julie . robin foobirds .org
^ ^D
```

In Listing 8.7, CallRulesets is passed the address julie@breast, which matches the $*@$-pattern of the first rule in the ruleset. That rule callset canonify and passes the three tokens @, and breast. canonify “focuses” the address by placing angle brackets around the host portion, and in turn, callset canonify2. Canonify2 converts the address to julie@robin.foobirds.org>, which is the value that canonify returns to CallRulesets. The second rule in CallRulesets is executed. The value julie@robin.foobirds.org> matches the $@ pattern in the rule, so rule final is called and passed the address value. final “defocuses” the address and returns the value julie@robin.foobirds.org, which becomes the value returned by CallRuleset.

NOTE The "focus" and "defocus" are used to describe the internal Sendmail processes that mark portions of the address for processing. Generally, this involves enclosing address in angle brackets.

# Transforming Addresses with External Information

In Listing 8.7, CallRule simply matches the patterns and calls other rulesets to do all of the rewriting. It is also possible to use an external server, such as DNS, or an external database to convert an input address. The Canary rules converts a hostname to the canonical DNS format for hostname. It does this by querying DNS and using information it gets in response to that query.

The [$hostname] syntax converts a host's nickname or its IP address to its canonical name by passing the hostname to the name server for resolution. Listing 8.8 shows the [$hostname] symbol in action.

# Listing 8.8 Retrieving a Canonical Name from DNS

```
[root]# mail -bt -Ctest.cf
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> CallRulesets julie@red
CallRulesets      input: julie @ broadest
canonify          input: julie @ broadest
canonify2         input: julie < @ broadest
canonify2         returns: julie < robin foobirds .org >
canonify          returns: julie . robin foobirds .org >
final             input: julie < robin foobirds .org >
final             returns: julie . robin foobirds .org
CallRulesets      returns: julie . robin foobirds .org
^ ^D
```

In Listing 8.7, CallRule simply matches the patterns and calls other rulesets to do all of the rewriting. It is also possible to use an external server, such as DNS, or an external database to convert an input address. The Canary rules converts a hostname to the canonical DNS format for hostname. It does this by querying DNS and using information it gets in response to that query.

The [$hostname] syntax converts a host's nickname or its IP address to its canonical name by passing the hostname to the name server for resolution. Listing 8.8 shows the [$hostname] symbol in action.

In the same way that a hostname or address is used to look up a canonical name in the name database, the $(database-spec) syntax allows you to retrieve information from a database. This is a more generalized database retrieval syntax than the one returns hostnames, and it is more complex to use. To transform an argument in a rewrite rule, include the database in the template part of a rule with the following syntax:

```
map key [@argument...] $:default$
```

map is the name assigned to the database by a K command. Like mailers, map names are arbitrary names used only inside the sendmail.cf file. The map name used in the rewrite template must match the name assigned to the database by the K command. Because K commands are the result of the m4 FEATURE commands used to create the configuration, the map names are the same on Linux systems. (Chapter 7 for a description of the K command syntax).

key is the value used to index into the database. The value returned from the database for this key is used to rewrite the input address. If no value is returned, the input address is changed to the key unless a default value is provided using the $:default syntax.

An argument is a value passed to the database by the key. Multiple arguments can be used, but each argument must start with $. The argument modifies the value returned to Sendmail. Arguments are referenced as %n, where n is a digit that indicates the order in which the argument appears in the string of arguments, when multiple arguments are used. Argument %0 is the key, %1 is the first argument, %2

# Rewrite Rules 239

In Listing 8.8, the key is julie@breast. $1 contains julie and $2 contains breast. The query for breast returns robin foobirds.org. The second test is even more interesting because it demonstrates that e-mail can be addressed with an IP address instead of a hostname. This passes 172.1.5 to the ruleset. If an address has a PTR record, it can be mapped back to a name.

TIP Not sure about DNS CNAME records and PTR records? See DNS Server Administration by Craig Hunt (Sybex, 2000), which is also part of the Craig Hunt Library.
