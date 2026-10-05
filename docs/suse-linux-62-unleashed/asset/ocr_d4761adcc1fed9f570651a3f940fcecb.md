# SMTP and Protocols
CHAPTER 9 297

invoking ruleset 3 manually is a good idea because later rulesets expect the address to be in canonical form.

The > prompt sendmail is waiting for you to enter one or more ruleset numbers, separated by commas, and an address. Try your login name with rules 3 and 0. The result should look like this:

```
> 3,0 joe
rewrite: ruleset 3 input: joe
rewrite: ruleset 3 returns: joe
rewrite: ruleset 0 input: joe
rewrite: ruleset 3 input: joe
rewrite: ruleset 3 returns: joe
rewrite: ruleset 2 input: joe
rewrite: ruleset 3 returns: joe
rewrite: ruleset 0 returns: $ local: joe >
```

The output shows how sendmail processes the input joe in each ruleset. Each line of output is identified with the name of the ruleset processing, the input address, and the address that the ruleset returns. The > is a second prompt indicating that sendmail is waiting for another line of input. When you're done testing, just press Ctrl+D.

Indentation and blank lines show the flow of processing in this example:

```
rewrite: ruleset 3 input: joe
rewrite: ruleset 3 returns: joe
```

```
rewrite: ruleset 0 input: joe
```

```
rewrite: ruleset 3 input: joe
rewrite: ruleset 3 returns: joe
```

```
rewrite: ruleset 6 input: joe
rewrite: ruleset 6 returns: joe
```

```
rewrite: ruleset 0 returns: $ local: joe
```

The rulesets called were 3 and 0, in order. Ruleset 3 was processed and returned the value joe, and then sendmail called ruleset 0. Ruleset 0 called ruleset 3 again and then ruleset 6, an example of how a ruleset can call another one by using $. Neither ruleset 3 nor ruleset 6 rewrote the input address. Finally, ruleset 0 resolved to a mailer, as it must.

![](bbox=[0.888, 0.614, 0.966, 0.755])