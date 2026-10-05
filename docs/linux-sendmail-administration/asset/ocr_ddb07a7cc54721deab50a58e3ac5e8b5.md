# Testing Your New Configuration 213

```
canonify input: craig
Canonify2 input: craig
Canonify2 returns: craig
canonify returns: craig
1 input: craig
1 returns: craig
HdrFromSMTP input: craig
PseudoToReal input: craig
PseudoToReal returns: craig
MasqSMTP returns: craig < @LOCAL*
MasqHdr input: craig < @LOCAL*
MqHdr returns: craig < @ parrot . foobirds . org >
HdrFromSMTP returns: craig < @ parrot . foobirds . org >
final input: < @ parrot . foobirds . org >
final returns: craig < @ parrot . foobirds .org
Rcode = 0, addr = craig@parrot.foobirds.org
```

> NOTE These tests run with Sendmail 8.11. The output from older versions of Sendmail, which used ruleset numbers instead of names, will look slightly different.

The address returned by ruleset final, which is always the last ruleset to process an address, shows the address that will be used on outbound mail after all of the ruleset have processed the address. With the default configuration, the input address craig@parrot.foobirds.org.

> NOTE Ruleset final is also known as ruleset 4.

![](bbox=[0.916, 0.452, 0.981, 0.538])