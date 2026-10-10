When the pattern matches the word `cat`, "cat" appears in the substituted word. When it matches the word `hat`, "hat" appears in the substituted word.

# Replac ing individual words

The ampersand symbol retrieves the entire string that matches the pattern you specify in the substitution command. Sometimes, you'll want to retrieve only a subset of the string. You can do that, too, but it's a little tricky.

The `sed` editor uses parentheses to define a substring component within the substitution pattern. You can then reference each substring component using a special character in the replacement pattern. The replacement character consists of a backslash and a number. The number indicates the substring component's position. The `sed` editor assigns the first component the character `\_1`, the second component the character `\_2`, and so on.

# NOTE

When you use parentheses in the substitution command, you must use the escape character to identify them as *grouping* characters and not normal parentheses. This is the reverse of when you escape other special characters.

Look at an example of using this feature in a `sed` editor script:

```
$ echo "The Guide to Programming" | > sed ' s/\(Guide to\) Programming/\1 DevOps/' The Guide to DevOps $
```

This substitution command uses one set of parentheses around `Guide To` to identifying it as a substring component. It then uses the `\_1` in the replacement pattern to recall the first identified component. This isn't too exciting, but it can really be useful when working with wildcard patterns.

Suppose you need to replace a phrase with just a single word that's a substring of the phrase, but that substring just happens to be using a wildcard character. In such cases, using substring components is a lifesaver:

```
$ echo "That furry cat is pretty." > sed 's/furry \(.at\)/\1/' That cat is pretty. $ echo "That furry hat is pretty." > sed 's/furry \(.at\)/\1/' That hat is pretty. $
```

In this situation, you can't use the ampersand symbol, because it would replace the entire matching pattern. The substring component provides the answer, allowing you to select just which part of the pattern to use as the replacement pattern.