```
egrep "\d" small.txt
```

## 0123456789

```
egrep "\s" small.txt
```

## aa bb cc
## tragedy + time = humor

As you can see in the example above, the \w metacharacter matches all letters, numbers, and even the underscore character (_). We can see the compliment of this grep by adding the -v flag to the command:

```
egrep -v "\w" small.txt
```

## %#&/=-*%*=-&%#

The -v flag (which stands for invert match) makes grep return all of the lines not matched by the regular expression. Note that the character sets for regular expressions also have their inverse sets: \W for non-words, \D for non-digits, and \S for non-spaces. Let’s take a look at using \W:

```
egrep "\W" small.txt
```