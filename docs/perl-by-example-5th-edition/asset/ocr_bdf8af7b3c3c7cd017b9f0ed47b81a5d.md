# EXAMPLE 8.6

```
```perl
(The Script)
use warnings;
1  while(<DATA>) {
2    print unless /Norma/;  # Print line if it doesn't match Norma
  }

3  __DATA__
Steve Blenheim
Betty Boop
Igor Chevsky
Norma Cord
Jon Deloach
Karen Evich

(Output)
Steve Blenheim
Betty Boop
Igor Chevsky
Jon Deloach
Karen Evich
```
```

# EXPLANATION

+   * 2 All lines that don't contain the pattern *Norma* are matched and printed. (Similar to the `grep -v` command for UNIX.)
+   * 3 The DATA filehandle gets its data from the lines that follow the `__DATA__` token.

# 8.3 Regular Expression Operators

The regular expression operators are used for matching patterns in searches and for replacements in substitution operations. The *m* operator is used for matching patterns, and the *s* operator is used when substituting one pattern for another.

# 8.3.1 The *m* Operator and Pattern Matching

The *m* operator is optional if the delimiters enclosing the regular expression are forward slashes (the forward slash is the default), but required if you change the delimiter. You may want to change the delimiter if the regular expression itself contains forward slashes (for example, when searching for birthdays, such as 3/15/93, or pathnames, such as */usr/var/adm*). Matching modifiers are shown in Table 8.2.