
## Chapter 8 Understanding Rewrite Rules

rule. At first glance, one might think that flow control is not required for that because it is the last rule in the ruleset and thus the ruleset will end after rule executes. On closer examination the principle is clear: the third rule will never finish executing because it is an infinite loop. The $* pattern matches zero or more tokens, meaning it will match anything, the string Wrong format, the pattern will match the output of the rule. Because the rule recursively processes its output against the pattern $, which matches anything, a loop will ensue. Sendmail detects loops and complaints when one is found, in Listing 8.6.

### Listing 8.6 Results of a Tight Loop in the Sendmail Configuration

```
[root]# sendmail -bt -Ctest.cf
ADDRESS TEST TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> =ClassTest
R$ = $*                        @ Found it
R$ = $w                        @ Not in class w
R$                               Wrong format
> ClassTest craig
ClassTest input: craig
Infinite loop in ruleset ClassTest, rule 3
ClassTest returns: Wrong format
> ^D
```

In Listing 8.6, sendmail is again run with the -bt -S command, described in Chapter 10 with other test commands, is used to display the contents of the ruleset ClassTest. In this example, the template in the third rule of the ruleset does not start with $. In this case, when ClassTest is run with an input of craig, an infinite loop ensues. Sendmail displays an error message stating that an infinite loop was encountered and exactly where the loop occurred.

Loops do not need to be as tight as the one shown in Listing 8.6. A loop can involve multiple rules because a ruleset can be called by a rule using the $>name syntax. When the called ruleset finishes processing, it returns a rewritten address to the calling rule. The returned e-mail address is then compared to the pattern in the calling rule. If it still matches, the ruleset is called again. Use $: and $@ to prevent loops whenever they can occur.

## Rewrite Rules 237

The $>name symbol calls ruleset name and passes the address defined by the remainder of the template for processing. For example, both rules in the ruleset named CallRulesets, shown below, call other rulesets:

```
SCallRulesets
R$* @ $- $: $> canonify $1 @ $2
R$* $: $> final $1
```

The template in the first rule calls canonify($canonify), and passes the contents of $1, a literal @, and the contents of $2. The template starts with the $: symbol, so the first rule executes only when the pattern matches. The template in the second rule calls final($final) and passes the contents of $1. (Because the pattern in the second rule includes only one symbol, $1 contains the entire input address.) The second rule will also only execute once because its template starts with $: Listing 8.7 shows the CallRulesets rules in action.

### 8.7 Calling Another Ruleset from a Rule

```
[root]# sendmail -Ctest.cf
ADDRESS TEST MODE <address>
-ter <ruleset> <address>
> CallRulesets julieredbreast
CallRulesets input: julie redbreast
canonify input: julie <: breast>
Canonify2 input: julie <: breast>
canonify returns: julie @robin . foobirds .org . > returns: julie @robin . foobirds .org . >
final input: julie @robin . foobirds .org . >
final returns: julie @robin . foobirds .org
CallRulesets returns: julie @robin . foobirds .org
> ^
```

In 8.7, CallRulesets is passed the address julieredbreast, which matches the $@-pattern of the first rule in the ruleset. That rule calls ruleset canonify and passes the three tokens: julie, @, and redbreast. Canonify “focuses” the address by placing angle brackets around the host and in turn, it calls ruleset Canonify2 which converts the address to julie@robin.foobirds.org>, which is the value that canonify returns to CallRulesets. The second rule in CallRulesets is then executed. The value julie@robin.foobirds.org> matches the $@ pattern in the rule, so ruleset final is called and passed the address value. final “defocuses” the address and returns the value julie@robin.foobirds.org, which becomes the value returned by CallRuleset.

![](img/b8082498451dba2bf0cf2907c85c4c83_257_0.png)

## 238 Chapter 8 Understanding Rewrite Rules

> NOTE The words "focus" and "defocus" are used to describe the internal Sendmail processes that mark portions of the address for processing. Generally, this involves enclosing address components in angle brackets.

## Transforming Addresses with External Information

In Listing 8.7, Call1Ruleset simply matches the patterns and calls other rulesets to do all of the rewriting. It is also possible to use an external server, such as DNS, or an external database to convert an input address. The Canonify2 ruleset converts a hostname to the canonical DNS format for that. This is done by querying DNS and using the information it gets in response to that query.

The [$hostname] syntax converts a nickname or its IP address to the canonical name by passing the virtual hostname to the server for resolution. Listing 8.8 shows the [$hostname] symbol in.

### Listing 8.8 Retrieving a Canonical Name from DNS

```
[root]# sendmail -bt -Ctest.cf
ADDRESS MODE 3 NOT automatically invoked
 Enter <ruleset> <address>
 >=SDNTest
R$ @ $+ $:1 @ $[2 $\$
> DNTest julie @ redbreast
DNTest input: julie @ redbreast
returns: julie @ robin . fobirds . org
> DNTest julie@[172.16.5.2]
DNTest input: julie @ [ 172 . 16 . 5 . 2 ]
returns: julie @ robin . fobirds . org
> ^
```

The test.cf configuration file in Listing 8.8 contains a very simple ruleset named DNTest, which is displayed by the $SDNTest command. The ruleset has only one rewrite rule. The rule matches any address that contains zero or more tokens, a literal @, and one more tokens. The template in the rule is:

$:1 @ $[2$ ensures that the rule runs only once. The $1 symbol and the literal @ guarantee that any tokens occurring before the @ in the input address and itself are replicated in the output address. The symbols [$ and ] enclose the value passed to DNS, which is the second indefinite token created by the pattern match. $2 includes all of the tokens after the literal @ in the input address.

## Rewrite Rules 239

In Listing 8.8, the first value passed to the rule is julie@redbreast. After the pattern match, $1 contains julie and $2 contains redbreast. The DNS query returns robin.foobirds.org as the name server has a CNAME record for redbreast that indicates that robin is its canonical.

The second test is even more interesting because it demonstrates that e-mail can be addressed with an IP address of a hostname. That test passes the address julie@[172.16.5.2] to the DNSTest rules. Clearly 172.16.5.2 is not a hostname; it is an IP address. In this case DNS is asked to return the canonical name for the address. If DNS has a PTR record for the PTR record, the address can be mapped back to a name. In case, it does the query for 172.16.5.2 returns the canonical name foobirds.org.

> TIP Not about DNS CNAME records and PTR records? See Linux Server Administration by Craig Hunt (Sybench, 2000), which is also part of the Craig Library.

In the same way that a hostname or address is used to look up a canonical name in the name server, the $(database-spec) syntax allows to retrieve information from a database. This is a more generalized database retrieval than the one that returns hostnames, and it is more complex to use. To use an external database to transform an address rewrite rule, include the database in the template part of a rule with the following syntax:

```
$(map key [@argument...] [$default $)
```

map is the name assigned to the database by a k command. Like mailer, map names are arbitrary names only used inside of sendmail.cf file. The map name used in the rewrite template must match the name assigned to the database by the K command. Most K commands are the result of the m4 FEATURE commands used to create the configuration, map names are the same on Linux systems. (See Chapter 7 for a description of the K command syntax).

key is the value used to index the database. The value returned from the database for this key is used to rewrite the input address. If no value is returned, the input address is changed to the key unless a default value is provided using the $:default syntax.

An argument is a value passed to the database program along with the key. Multiple arguments can be used, but each argument must start with $. The argument modifies the value returned to Sendmail. Arguments are referenced inside the database as %n, where n is a digit that indicates the order in which the argument appears in the string of arguments, when multiple arguments are used. Argument %0 is the key, %1 is the first argument, %2
