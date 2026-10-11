# EXAMPLE 9.13

```
```text
    (The Script)
    use warnings;
    # The \S metasyMBOL and nonwhitespace
1 while(<DATA>){
2     print if s/\S/ /g;
    }
    _ _ _DATA_ _ _
Steve Blenheim 101
Betty Boop 201
Igor Chevyky 301
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
```

# EXPLANATION

The line  _is printed if_s matches a pattern containing a nonwhitespace character (not a space, tab, or newline), \S. This time, all nonwhitespace characters are replaced with an * . When a metasyMBOL is capitalized, it negates the meaning of the lowercase version of the metasyMBOL; \D is a digit; \d is a nondigit.

# EXAMPLE 9.14

```
```text
    (The Script)
    use warnings;
    # Escape sequences, \n and \t
1 while(<DATA>){
2     print if s/\n/\t/;
    }
    _ _ _DATA_ _ _
Steve Blenheim 101
Betty Boop 201
Igor Chevyky 301
Norma Cord 401
Jonathon DeLoach 501
Karen Evich 601

(Output)
Steve Blenheim 101  Betty Boop 201  Igor Chevyky 301
Norma Cord 401  Jon DeLoach 501  Karen Evich 601
```
```