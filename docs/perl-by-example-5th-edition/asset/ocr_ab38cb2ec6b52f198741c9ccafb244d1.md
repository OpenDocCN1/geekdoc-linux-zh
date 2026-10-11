# ## 8.3 Regular Expression Operators

# **EXAMPLE 8.23 (CONTINUED)**

(Output)

    Steve Blenheim   5
    Betty Boop        4
    Igor Chevalky     43.8
    Norma Cord        1
    Jon DeLoach       3
    Karen Enich       43.843.8

# **EXPLANATION**

+   2 If the `$` scalar contains the number 6, the replacement side of the substitution is evaluated. In other words, the 6 is multiplied by 7.3 (e modifier); the product of the multiplication (43.8) replaces the number 6 each time the number 6 is found (g modifier).
+   3 Each line is printed. The last line contained two occurrences of 6, causing each 6 to be replaced with 43.8.

# **EXAMPLE 8.25**

```
(The Script)

```
    use warnings;
    # The e modifier
    1 my $number = 5;
    2 s/6 * 4 - 22/e;
    3 print "The result is: $number\n";
    
    4 $number = 51055;
    5 s/5/3 * 2/e;
    6 print "The result is: $number\n";
    
    (Output)
    3 The result is: 2
    6 The result is: 61066
```
```

# **EXPLANATION**

+   1 The `$number` scalar is assigned 5.
+   2 The `s` operator searches for the regular expression 5 in `$number`. The `e` modifier evaluates the replacement string as a numeric expression and replaces it with the result of the arithmetic operation, 6 * 4 - 22, that is, 2.
+   `$number` is assigned 1055.
+   5 The `s` operator searches for the regular expression 5 in `$number`. The `e` modifier evaluates the replacement string as a numeric expression and replaces it with the product of 3 * 2; that is, every time 5 is found, it is replaced with 6. Since the substitution is global, all occurrences of 5 are replaced with 6.