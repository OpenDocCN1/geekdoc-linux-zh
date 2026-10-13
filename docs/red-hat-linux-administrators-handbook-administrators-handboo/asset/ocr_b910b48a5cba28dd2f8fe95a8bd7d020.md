LHS is the left-hand-side pattern, and RHS is the right-hand-side pattern of the rule. For example, in the following syntax,

```
RS* < $* > $* <&>   $: $1 < $2 > $3
```

the LHS pattern is $* < $* > $* <&>, and the RHS pattern is $: $1 < $2 > $3. Both the LHS and RHS patterns are composed of various metasymbols, such as $*, $+, $-, $=x, and $-x.

Rewrite rules are quite complex and usually don't require any changes on your part. However, if you plan to write your own rewrite rules, you should read the Sendmail Installation and Operation Guide bundled with the sendmail documentation.

# D: define macro

D lines define a macro. The syntax is as follows:

```
D<macro name> <string>
```

For example, the following syntax is the same as $P = someword, and whenever $P is referenced elsewhere, it is expanded to someword:

```
DP someword
```

Typically, you do not need to add, delete, or remove any D macro definitions.

# C and F: define classes

C lines are similar to D lines. The syntax for such a line is as follows:

```
C<class name> <string> <string> . . .
```