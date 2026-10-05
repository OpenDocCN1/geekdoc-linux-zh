# Networking and Internet Services
PART II

```
# address delimiter characters
Do::%@![/]
```

All the characters in $ are both token separators and tokens. sendmail takes an address
such as rae@rainbow.org and breaks it into tokens according to the characters in the o
macro, like this:

+   * "rae", "@", "rainbow", \.", "org"

sendmail also parses the lhs of rewriting rules into tokens so they can be compared one
with the input address to see whether they match. For example, the lhs-
@rainbow.org is parsed as follows:

+   * "$", "@", "rainbow", \.", "org"

(Don't worry about the $ - just yet. It's a pattern-matching operator, similar to a shell
wildcard, that matches any single token and is covered later in the section "The Left-Hand
Side (lhs) of Rules." Now you put the two together to show how sendmail decides
whether an address matches the lhs of a rule:

+   * "rae", "@", "rainbow", \.", "org"

+   * "$", "@", "rainbow", \.", "org"

In this case, each token from the first line matches that of the second, thanks to the pattern-
matching operator ($ -), so the entire address matches and sendmail will use the rhs to
rewrite the address.

Consider the effect (usually bad) of changing the value of $. As shown previously,
sendmail breaks the address rae@rainbow.org into five tokens. However, if the @
character were not in s$, the address would be parsed quite differently, with only three
tokens:

+   * rae@rainbow", \.", "org"

You can see that changing $ has a drastic effect on sendmail's address parsing, and
would leave it alone until you know what you're doing. Even then, you probably won
want to change it because the V.8 sendmail configuration files already have it correctly
for standard RFC 822 and RFC 976 address interpretation.

# The Left-Hand Side (lhs)) of Rules

The lhs is a pattern against which sendmail matches the input address. The lhs can
contain ordinary text or any of the pattern-matching operators shown in Table 9.2.

TABLE 9.2 lhs Pattern-Matching Operators
$- | Match exactly one token.
+$ | Match one or more tokens.