## abcdefghijklmnopqrstuvwxyz
## rhythms
## tragedy + time = humor
## http://www.jhsph.edu/

```
egrep "[E-Q]" small.txt
```

## ABCDEFGHIJKLMNOPQRSTUVWXYZ

```
egrep "[e-qE-Q]" small.txt
```

## abcdefghijklmnopqrstuvwxyz
## ABCDEFGHIJKLMNOPQRSTUVWXYZ
## rhythms
## tragedy + time = humor
## http://www.jhsph.edu/

# Escaping, Anchors, Odds, and Ends

One issue you may have thought about during our little exploration of regular expressions is how to search for certain punctuation marks in text considering that those same symbols are used as metacharacters! For example, how would you find a plus sign (+) in a line of text since the plus sign is also a metacharacter? The answer is simply using a backslash (\ ) before the plus sign in a regex, in order to "escape" the metacharacter functionality. Here are a few examples: