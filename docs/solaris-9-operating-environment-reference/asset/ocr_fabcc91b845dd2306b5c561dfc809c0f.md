$(#parameter) String length. Specify the length, in characters, of the value of parameter: If parameter is * or @, substitute all the positional parameters, starting with $1 separated by a field separator character.

The four varieties of parameter expansion provide substring processing. In each case, pattern-matching notation (see pattern), instead of regular expression notation, is used to evaluate the patterns. If parameter is * or @, then all the positional parameters, starting with $1, are substituted (separated by a field separator character). Enclosing the full parameter expansion string in double quotes does not cause the following four varieties of pattern characters to be quoted, whereas characters within the braces does this effect.

$(parameter%word) Remove smallest suffix pattern. Expand word to produce a pattern. The parameter expansion then results in parameter, with the smallest portion of the suffix matched by the pattern deleted.

$(parameter##word) Remove largest suffix pattern. Expand word to produce a pattern. The parameter expansion then results in parameter, with the largest portion of the suffix matched by the pattern deleted.

$(parameter#word) Remove smallest prefix pattern. Expand word to produce a pattern. The parameter expansion then results in parameter, with the smallest portion of the prefix matched by the pattern deleted.

$(parameter##word) Remove largest prefix pattern. Expand word to produce a pattern. The parameter expansion then results in parameter, with the largest portion of the prefix matched by the pattern deleted.

# Pattern Expansion Examples

The following examples illustrate each of the pattern expansion forms. In the first example, ls is executed only if x is null or unset. (The $(ls) command notation is explained in "Command Substitution" on page 590.)

```
$(parameter:-word)
$(x:-$(ls))
```

```
$(parameter:=word)
unset X
echo \$(X:=abc)
abcabc
```

```
$(parameter??word)
unset posix
echo $(posix:?)
sh: posix:* parameter null or not set
```