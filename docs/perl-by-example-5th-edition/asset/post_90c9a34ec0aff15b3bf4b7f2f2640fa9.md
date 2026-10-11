
## Table 9.8 Look Around Assertions

| Metacharacter | What It Matches |
| :--- | :--- |
| /PATTERN(?=pattern)/ | Positive look ahead |
| /PATTERN(?!pattern)/ | Negative look ahead |
| (?<=pattern)/PATTERN/ | Positive look behind |
| (?<!pattern)/PATTERN/ | Negative look behind |

### EXAMPLE 9.44

(The Script)

```perl
use warnings;
# A positive look ahead
1 my $string="I love chocolate cake and chocolate ice cream.";
2 $string =~ s/chocolate (?=ice)/vanilla/;
3 print "$string\n";
4 $string="Tomorrow night Tom Savage and Tommy Johnson will leave
for vacation.";
5 $string =~ s/Tom(?=my)/Jere/g;
6 print "$string\n";
```

(Output)

```
3 I love chocolate cake and vanilla ice cream.
6 Tomorrow night Tom Savage and Jeremy Johnson will leave for vacation.
```

### EXPLANATION

1  The scalar `$string` contains chocolate twice; the word *cake* follows the first occurrence of *chocolate*, and the word *ice* follows the second occurrence.

2  This is an example of a *positive look ahead*. The pattern *chocolate* is followed by `(?=ice)`; meaning, if *chocolate* is found, look ahead `(?=)` and see if *ice* is the next pattern. If *ice* is found just ahead of *chocolate*, the match is successful and *chocolate* will be replaced with *vanilla*. The look ahead part, *ice*, is discarded. It is not part of the pattern to be replaced, but only there to help further define which *chocolate* we are looking for.

3  After the substitution on line 2, the new string is printed.

4  The scalar `$string` is assigned a string of text consisting of three words starting with *Tom*.

5  The pattern is matched if it contains *Tom*, only if *Tom* is followed by *my*. If the positive look ahead is successful, then *Tom* will be replaced with *Jere* in the string.

6  After the substitution on line 5, the new string is printed. *Tommy* has been replaced with *Jeremy*.

### EXAMPLE 9.45

```perl
# (The Script):
use warnings;
# A negative look ahead
while(<$DATA>){
    1 print if /^\w*\b(?! [BC] )/;
}
__DATA__
Steve Blenheim
Betty Boop
Igor Chevosky
Norma Cord
Jon DeLoach
Karen Evich
```

(Output):

```
Jon DeLoach
Karen Evich
```

### EXPLANATION

2  The regular expression means: search at the beginning of the line for one or more word characters (`\w+`), followed by a space (`\s`), and look ahead for any character that is not a B or C. This is called a negative look ahead.

### EXAMPLE 9.46

```perl
# (The Script):
use warnings;
# A positive look behind
1 my $string="I love chocolate cake, chocolate milk,
and chocolate ice cream.";
2 $string =~ s/(?<=chocolate) milk/ candy bars/;
3 print "$string\n";
4 $string="I love coffee, I love tea, I love the boys
and the boys love me.";
5 $string =~ s/(?<=the boys) love/ don't like/;
6 print "$string\n";
```

(Output):

```
3 I love chocolate cake, chocolate candy bars, and chocolate ice cream.
6 I love coffee, I love tea, I love the boys and the boys don't like me.
```

### EXPLANATION

1  The scalar `$string` is assigned a string with three different occurrences of chocolate.

2  The pattern in parentheses is called a **positive look behind**, meaning that Perl looks **backward** in the string to make sure this pattern occurs. If the pattern *milk* is found, Perl will look back in the string to see if it is preceded by *chocolate* and, if so, *milk* will be replaced with **candy bars**. The look behind pattern, *chocolate*, is not affected by the replacement, so now we have *chocolate candy bars*.

3  The string is printed after the substitution.

4  This is another example of a positive look behind. Perl looks backward in the string for the pattern *the boys*, and if the pattern is found, the regular expression *love* will be replaced with *don't like*.

### EXAMPLE 9.47

(The Script)

```perl
# A negative look behind
while(<DATA>){
    print if /(?<!Betty)\b[a-z]*/;
}
__DATA__
Steve Blenheim
Betty Boop
Igor Chevsuky
Norma Cord
Jon DeLoach
Karen Evich
```

(Output)

*Steve Blenheim*

### EXPLANATION

2  The pattern in parentheses is called a **negative look behind**, meaning that Perl looks **backward** in the string to make sure this pattern does not occur. Any line that contains the letter *B*, followed by zero or more lowercase letters, *[a-z]*, will be printed, as long as the pattern behind it is **not** *Betty*.

## 9.2.4 The tr or y Operators

The *tr* operator translates characters on a one-to-one basis. To see what this means, let’s compare translation to substitution. You can see in the following example that the syntax for both the *tr* operator and substitution operator look very much the same, but they are really quite different in what they do. Let’s take a look at **substitution** first:

```perl
$str = "Elizabeth likes little baby lizards. ";
$str =~ s/Elizabeth/Christopher/;
print "$str\n";
```

and the result is:

```
Christopher likes little baby lizards.
```

Now let's look at the *tr* function.

```perl
$str = "Elizabeth likes little baby lizards. ";
$str =~ tr/Elizabeth/Christoper/;
print "$str\n";
```

and the result is:

```
Christoph hkrzos hrpghpo tcty hrisrds.
```

What is different? The *s* operator searches for a pattern and replaces it with a string, meaning *Elizabeth* is replaced with *Christopher*. The *tr* operator translates characters, on a one-on-one correspondence, from each character in the search string to its corresponding character in the replacement string and returns the number of characters it replaced. In the preceding example, every E in `$str`, is translated to a corresponding C, every l is translated to an h, every i is translated to an r, and so on.

The *tr* operator does not interpret regular expression metacharacters but allows a dash (--) to represent a range of characters. The letter x can be used in place of tr. This strangeness comes from UNIX, where the *sed* utility has a y command to translate characters, similar to the UNIX tr. If you look at the UNIX *tr* man page, you can see that it is very similar to the Perl *tr* function, illustrating the role UNIX has played in the development of Perl.

The d option deletes the search string.

The c option complements the search string.

The s option is called the squeeze option. Multiple occurrences of characters found in the search string are replaced by a single occurrence of that character (for example, you may want to replace multiple tabs with single tabs). See Table 9.9 for a list of modifiers.

### Table 9.9 *tr* Modifiers

| Modifier | Meaning |
| :--- | :--- |
| d | Delete characters |
| c | Complement the search list |
| s | Squeeze out multiple characters to single character |

### FORMAT

```perl
tr/search/replacement/
tr/search/replacement/d
tr/search/replacement/c
tr/search/replacement/s
y/search/replacement/ (same as tr; uses same modifiers)
```

### EXAMPLE 9.48

```perl
# (The Input Data)
Steve Blenheim 101
Betty Boop 201
Igor Chevesky 301
Norma Cord 401
Jon DeLoach 501
Karen Evich 601

# (Lines from a Script)
1 tr/A-Z/a-z/; print;

(Output)
steve blenheim 101
betty boop 201
igor chevesky 301
norma cord 401
jon deloach 501
karen evich 601

2 tr/0-9/;/; print;

(Output)
Steve Blenheim ;;;
Betty Boop ;;;
Igor Chevesky ;;;
Norma Cord ;;;
Jon DeLoach ;;;
Karen Evich ;;;

3 tr/A-Z/a-c/; print;

(Output)
cteve blenhe1m 101
betsy boop 201
egor chevesky 301
corma cord 401
can cecooch 601
```

### EXAMPLE 9.48 (CONTINUED)

```perl
4 tr/ /# /; print;

(Output)
Steve#Blenheim#101
Betty#Boop#201
Igor#Chevsky#301
Norma#Cord#401
Jon#DeLoach#501
Karen#Evich#601

5 y/A-Z/a-z/; print;

(Output)
steve blenheim 101
betty boop 201
igor chevsky 301
norma cord 401
jon deloach 501
karen evich 601
```

### EXPLANATION

-   1. The *tr* operator makes a one-on-one correspondence between each character in the search string with each character in the replacement string. Each lowercase letter will be translated to its corresponding uppercase letter.
-   2. Each number will be translated to a semicolon.
-   3. The translation is messy here. Since the search side represents more characters than the replacement side, all letters from *D* to *Z* will be replaced with a *c*.
-   4. Each space will be replaced with pound signs (\#).
-   5. The *y* is a synonym for *tr*. Each uppercase letter is translated to its corresponding lowercase letter.

**The d (delete) Option.** The *d* (delete) option removes all characters in the search string not found in the replacement string.

### EXAMPLE 9.49

```perl
1 tr/ //; print; # Nothing happens

(Output)
1  Steve Blenheim
2  Betty Boop
3  Igor Chevsky
4  Norma Cord
5  Jon DeLoach
6  Karen Evich
```
