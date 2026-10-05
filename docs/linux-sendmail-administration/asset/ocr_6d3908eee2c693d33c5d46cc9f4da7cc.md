# Rewrite Rules 227

# Table 8.3 Pattern-Matching Symbols (continued)

| Symbol | Meaning |
| $x | Match any token in class variable x. |
| $\~x$ | Match any token not in class variable x. |

All of the symbols match number of tokens. A token is a string of characters delimited by an operator. The operators are the right (() and left (()) parentheses, right (<) and left (>) brackets, comma (,), semicolon (;), backslash (\), quotation mark ("), carriage return (CR), and line feed (LF), plus any characters defined by the OperatorChars option. A grep of sendmail.cf for OperatorChars shows the additional operator characters are ; % @ ! ^ [ ] and ,

```
grep 'OperatorChars' /etc/sendmail.cf
0 OperatorChars=;%@!^]+
```

Operators also count as tokens when an address is parsed. Assume the following address:
sara@hawk.foobirds.org
This-mail address contains seven tokens: sara, @, hawk, foobirds, and three. Of these two, . (dots) and @ are operators. The other four tokens are strings. This address would match the symbol $ because it contains more than one token, but it would not match the Table 8.3 $ because it does not count exactly one token.

The symbols in Table 8.3 are particularly useful when paired with literal values and variables to create more complex patterns--for example:
$- @$-foobirds.org
The sample address sara@hawk.foobirds.org matches the pattern because:
- It has exactly one token before the literal @ that matches the requirement of the $-
- It has an @ that matches the pattern's literal @.
- It has exactly one token after the literal @ and before the literal .foobirds.org that matches the requirement of the second $ symbol.
- It has the string .foobirds.org that matches the pattern's literal .foobirds.org.
sara@hawk.foobirds.org matches this pattern, but many other addresses do not. For example, sara.hanson@hawk.foobirds.org does not match because it has three tokens, sara, ,, and henson before the literal @. Therefore, it fails to meet the requirement of

![](bbox=[0.915, 0.453, 0.985, 0.542])