the literal string wren.foobirds.org. In reality the rule contains $j, so the string wren.foobirds.org must be the value stored in the j on our sample system. Generally, the =S command is used to examine a ruleset if it sees the changes you made to the ruleset appear as you expect, or because you're trying to figure out how a ruleset does what it does.

To really examine the details of a ruleset in action, you can use a debug mode. The -d command to select a debug level inside of address test mode. Listing 10.14 shows a test with without debug mode 21.12.

# Listing 10.14 Using a Debug Setting during Address Test Mode

```
[root]# sendmail -bt
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
nEnter<ruleset> <address>
> final sara < foobirds .org >
    input: sara < foobirds .org >
final
    returns: sara < foobirds .org
>-d21.12
> final sara < foobirds .org >
final
    input: sara < foobirds .org >
----trying rule: $* < $+ $*
----rule fails
----trying rule: $* < $+ > $*
----rule matches: $1 < $2 > $3
rewritten as: sara < foobirds . org
----trying rule: $* < $+ > $*
----rule fails
----trying rule: $* < *LOCAL* > $*
----rule fails
----trying rule: $* < $+ > $*
----rule matches: $1 < $2 > $3
rewritten as: sara < foobirds . org
----trying rule: $* < $+ > $*
----rule fails
----trying rule: $@ < : $@ $+ : $+
----rule fails
----trying rule: @ $* 
----rule fails
----trying rule: $* < $+ $- . UUCP
----rule fails
```