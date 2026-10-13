This runs sendmail in address mode and provides you a prompt to interact with it. At the prompt, enter a test command, such as the following:

```
<rewrite rule #s> <test address>
```

For example, to see what sendmail's rewrite rule 0 does with kabir@nitec.com, run the following:

```
0 kabir@nitec.com
```

The output on my sendmail system is shown here:

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 0 kabir@nitec.com
rewrite: ruleset 0 input: kabir @ nitec . com
rewrite: ruleset 199 input: kabir @ nitec . com
rewrite: ruleset 199 returns: kabir @ nitec . com
rewrite: ruleset 98 input: kabir @ nitec . com
rewrite: ruleset 98 returns: kabir @ nitec . com
rewrite: ruleset 198 input: kabir @ nitec . com
rewrite: ruleset 198 returns: $# local $: kabir @ nitec . com
rewrite: ruleset 0 returns: $# local $: kabir @ nitec . com
```

The kabir@nitec.com address is delivered using the local mailer.

Consider another example, in which you have the following /etc/mail/ domaintable map:

```
ad-engine.com nitec.com
```

The preceding map routes all mail destined for ad-engine.com to nitec.com. The following example tests this map:

```
ADDRESS TEST MODE (ruleset 3 NOT automatically invoked)
Enter <ruleset> <address>
> 3,0 kabir@nitec.com
rewrite: ruleset 3 input: kabir @ nitec . com
rewrite: ruleset 96 input: kabir < @ nitec . com >
```