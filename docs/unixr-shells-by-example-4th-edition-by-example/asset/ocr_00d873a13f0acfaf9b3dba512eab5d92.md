# EXAMPLE 13.73 (CONTINUED)

```
hi there
how are you?
When will this end?
When the quote is matched
oh
```

```
2 $ echo Don\'t you need '$5.00'?
Don\'t you need $5.00?
```

```
3 $ echo 'Mother yelled, "Time to eat!"'
Mother yelled, "Time to eat!"
```

# EXPLANATION

+   1 The single quote is not matched on the line. The bash shell produces a secondary prompt. It is waiting for the quote to be matched.
+   2 The single quotes protect all metacharacters from interpretation. The apostrophe in Don\'t is escaped with a backslash (the backslash protects a single character, rather than a string). Otherwise, it would match the single quote before the $. Then the single quote at the end of the string would not have a mate. The $ and the ? are enclosed in a pair of single quotes, protecting them from shell interpretation, thus treating them as literals.
+   3 The single quotes protect the double quotes in this string.

# 13.11.3 Double Quotes

Double quotes must be matched, will allow variable and command substitution, and protect any other special metacharacters from being interpreted by the shell.

# EXAMPLE 13.74

```
1 $ name=Jody
```

```
2 $ echo "Hi $name, I'm glad to meet you!"
Hi Jody, I'm glad to meet you!
```

```
3 $ echo "Hey $name, the time is $(date)"
Hey Jody, the time is Wed Jul 14 14:04:11 PST 2004
```

# EXPLANATION

+   1 The variable name is assigned the string Jody.
+   2 The double quotes surrounding the string will protect all special metacharacters from interpretation, with the exception of $ in $name. Variable substitution is performed within double quotes.
+   3 Variable substitution and command substitution are both performed when enclosed within double quotes. The variable name is expanded, and the command in parentheses, date, is executed. (See "Command Substitution," next.)