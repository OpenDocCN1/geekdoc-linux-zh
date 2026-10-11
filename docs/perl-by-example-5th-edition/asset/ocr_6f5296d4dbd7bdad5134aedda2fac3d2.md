# EXAMPLE 9.27 (CONTINUED)

```
_DATA_
Steve Blenheim 1.10
Betty Boop .5
Igor Chevyvsky 555.100
Norma Cord 4.01
Jonathan DeLoach .501
Karen Evich 601

(Output)
Jonathan DeLoach .501
```

# EXPLANATION

The regular expression contains the `\b` metacharacter, representing a word boundary. The expression reads: find a word beginning with the pattern *Jon*.

# EXAMPLE 9.28

```
(The Script)
use warnings;
# Beginning- and end-of-word anchors
1 while (<DATA>){
2 print if /\bJon\b/;
}

_DATA_
Steve Blenheim 1.10
Betty Boop .5
Igor Chevyvsky 555.100
Norma Cord 4.01
Jonathan DeLoach .501
Karen Evich 601

(Output)
<No output>
```

# EXPLANATION

The regular expression also contains the `\b` metacharacter, representing a word boundary. The expression reads: find a word beginning and ending with *Jon*. Nothing is found.

**The *m* Modifier.** The *m* modifier is used to control the behavior of the `$` and `^` anchor metacharacters. A string containing newlines will be treated as multiple lines. If the regular expression is anchored with the `^` metacharacter, and that pattern is found at the beginning of any one of the multiple lines, the match is successful. Likewise, if the regular expression is anchored by the `$` metacharacter (or `\Z`) at the end of any one of the multiple lines, and the pattern is found, it too will return a successful match. The *m* modifier has no effect with `\A` and `\z`.