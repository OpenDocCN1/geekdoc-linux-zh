
## EXAMPLE 9.13

```perl
use warnings;
# The \S metacharacter and nonwhitespace
1 while(<DATA>){
2     print if s/\S/ /g;
    }
__DATA__
Steve Blenheim 101
Betty Boop 201
Igor Chevalier 301
Norma Cord 401
Jonathon DeLoach 501
Karen Evich 601

(Output)
********* **** **** ****
**** **** ****
**** *** **** ****
********* **** ****
******** ****
```

### EXPLANATION

The line is printed if `$_` matches a pattern containing a nonwhitespace character (not a space, tab, or newline), `\S`. This time, all nonwhitespace characters are replaced with an `*`. When a metacharacter is capitalized, it negates the meaning of the lowercase version of the metacharacter; `\D` is a digit; `\d` is a nondigit.

## EXAMPLE 9.14

```perl
use warnings;
# Escape sequences, \n and \t
1 while(<DATA>){
2     print if s/\n/\t/;
    }
__DATA__
Steve Blenheim 101
Betty Boop 201
Igor Chevalier 301
Norma Cord 401
Jonathon DeLoach 501
Karen Evich 601

(Output)
Steve Blenheim 101\tBetty Boop 201\tIgor Chevalier 301
Norma Cord 401\tJon DeLoach 501\tKaren Evich 601
```

### EXPLANATION

The regular expression contains the `\n` escape sequence, representing a single newline character. The expression reads: print the line if the substitution is successful; meaning, each newline can be replaced with a tab (`\t`).

### 9.2.3 Metacharacters to Repeat Pattern Matches

In the previous examples, the metacharacter matched on a single character. What if you want to match on more than one character? For example, let's say you are looking for all lines containing names, and the first letter must be in uppercase—which can be represented as `[A-Z]`—but the following letters are lowercase, and the number of letters varies in each name. `[a-z]` matches on a single lowercase letter. How can you match on one or more lowercase letters? Or zero or more lowercase letters? To do this, you can use what are called **quantifiers**. To match on one or more lowercase letters, the regular expression can be written `/[a-z]+/` where the `+` sign means “one or more of the previous characters,” which in this case is one or more lowercase letters. Perl provides a number of quantifiers, as shown in Table 9.5.

**Table 9.5 The Greedy Metacharacters**

| Metacharacter | What It Matches |
| :--- | :--- |
| `x?` | Matches 0 or 1 occurrences of x |
| `(xyz)?` | Matches 0 or 1 occurrences of pattern xyz |
| `x*` | Matches 0 or more occurrences of x |
| `(xyz)*` | Matches 0 or more occurrences of pattern xyz |
| `x+` | Matches 1 or more occurrences of x |
| `(xyz)+` | Matches 1 or more occurrences of pattern xyz |
| `x{m,n}` | Matches at least m occurrences of x and no more than n occurrences of x |

**The Greed Factor.** Normally, quantifiers are *greedy*; in other words, they match on the largest possible set of characters starting at the left-hand side of the string and searching to the right, look for the last possible character that would satisfy the condition. For example, given the following string:

```perl
$s="ab123456783445554437AB"
```

and the regular expression

```perl
m/ab[0-9]*X/;
```

the search side would match `ab123456783445554437`. All of this will be replaced with an `X`. After the substitution, `$_` would be `XAB`.

The asterisk (`*`) is a greedy metacharacter. It matches for zero or more of the preceding characters. In other words, it attaches itself to the character preceding it and looks only for zero or more occurrences of that character. In the preceding example, the asterisk attaches itself to the character class `[0-9]`. The matching starts on the left, searching for `ab` followed by zero or more numbers in the range between 0 and 9. The matching continues until the last number is found; in this example, the number 7. The pattern `ab` and all of the numbers in the range between 0 and 9 are replaced with a single `X`. The trailing characters, `AB`, remain.

Greediness can be turned off so that instead of matching on the greatest number of characters, the match is made on the least number of characters found. This is done by appending a question mark after the greedy metacharacter (see Example 9.23).

## EXAMPLE 9.15

```perl
use warnings;
# The zero or one quantifier
1  while(<DATA>) {
2  print if /[0-9]+.?/;
}

__DATA__
Steve Blenheim 1.10
Betty Boop .5
Igor Chevalier 555.100
Norma Cord 4.01
Jonathon DeLoach .501
Karen Erich 601

(Output)
Steve Blenheim 1.10
Igor Chevalier 555.100
Norma Cord 4.01
Karen Erich 601
```

### EXPLANATION

- The regular expression contains the `?` metacharacter, representing zero or one of the preceding characters. The expression reads: find a space, followed by a number between 0 and 9, followed by either one literal period or no period at all.

## EXAMPLE 9.16

```perl
use warnings;

# The zero or one quantifier
1 while(<DATA>){
2 print if /\sB[a-z]*/ ;

}

__DATA__
Steve Blenheim 1.10

Betty Boop .5

Igor Chevalier 555.100

Norma Cord 4.01

Jonathan DeLoach .501

Karen Evich 601

(Output)
Steve Blenheim 1.10

Betty Boop .5
```

### EXPLANATION

- The regular expression contains the `*` metacharacter, representing zero or more of the preceding character. The expression reads: Find a space, `\s`, followed by a `B` and zero or more lowercase letters `[a-z]*`.

## EXAMPLE 9.17

```perl
use warnings;

# The dot metacharacter and the zero or one quantifier
1 while(<DATA>){
2 print if s/[A-Z]*/y/Tom/ ;

}

__DATA__
Steve Blenheim 101

Betty Boop 201

Igor Chevalier 301

Norma Cord 401

Jonathan DeLoach 501

Karen Evich 601

(Output)
Tom Boop 201

Tom 301
```

### EXPLANATION

- The regular expression contains `.*`, where the `*` represents zero or more of the previous character. In this example, the previous character is the dot metacharacter, which represents any character at all. This expression reads: find an uppercase letter, `[A-Z]`, followed by zero or more of any character, `.*`, followed by the letter `y`. If there is more than one `y` on the line, the search will include all characters up until the *last* `y`. Both *Betty* and *Igor Chevalier* are matched. Note that the space in *Igor Chevalier* is included as one of the characters matched by the dot metacharacter.

## EXAMPLE 9.18

```perl
use warnings;
# The one or more quantifier
1  while(<DATA>){
2     print if /5+/;
  }
__DATA__
Steve Blenheim 1.10
Betty Boop .5
Igor Chevalier 555.100
Norma Cord 4.01
Jonathon DeLoach .501
Karen Evich 601

(Output)
*Betty Boop .5*
*Igor Chevalier 555.100*
*Jonathon DeLoach .501*
```

### EXPLANATION

- The regular expression contains the `+` metacharacter, representing one or more of the preceding characters. The expression reads: Find one or more repeating occurrence of the number 5.

## EXAMPLE 9.19

```perl
use warnings;
# The one or more quantifier
1  while(<DATA>){
    print if m/\w+/X/g;
2  }

__DATA__
Steve Blenheim 101
Betty Boop 201
Igor Chevalier 301
Norma Cord 401
Jonathan DeLoach 501
Karen Evich 601

(Output)
X X X
X X X
X X X
X X X
X X X
X X X
```

### EXPLANATION

The regular expression contains `\w` followed by a `+` metacharacter, representing one or more alphanumeric word characters. For example, the first set of alphanumeric word characters is *Steve*, and *Steve* is replaced by an `X`. Since the substitution is global, the next set of alphanumeric characters, *Blenheim*, is replaced by an `X`. Finally, the alphanumeric characters, `101`, are replaced by an `X`.

## EXAMPLE 9.20

```perl
use warnings;
# Repeating patterns
while(<$DATA>) { print if / \d{1,3}/;
}
__DATA__
Steve Blenheim 1.10
Betty Boop .5
Igor Chevalier 555 .100
Norma Cord 4 .01
Jonathan DeLoach .501
Karen Evich 601

(Output)
Betty Boop .5
Igor Chevalier 555 .100
Jonathan DeLoach .501
```

### EXPLANATION

- The regular expression contains the curly brace `{}` metacharacters, representing the number of times the preceding expression will be repeated. The expression reads: find at least one occurrence of the pattern `\d` and as many as three in a row.
