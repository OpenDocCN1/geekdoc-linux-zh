If you need to use a metacharacter as a normal character in the regular expression, you can use the \metachar format to take away the special meaning. An example of this is \$ , which is a regular dollar sign character. The standard quantifiers used in regular expressions are shown in Table B-2.

| Table B-2 Standard Quantifiers | | 
| Quantifier | Meaning | 
| * | Match 0 or more times | 
| + | Match 1 or more times | 
| ? | Match 1 or 0 times | 
| {n} | Match exactly $n$ times | 
| {n,} | Match at least $n$ times | 
| {n, m} | Match at least $n$ but not more than $m$ times |

A \| character is treated as an OR operator. A pair of parentheses () enables you to define the area used for the search match strings in a regular expression. A pair of square brackets [ ] creates a character class or range.

Let’s revisit the first example again:

```
`(([a-z])+)+\.([a-z])+\.([a-z])+`
```

As mentioned before, this expression can be used to match strings such as `www.hungryminds.com`. The first `[a-z]+` specifies that one or more characters in the a to z range is needed to match the group specified by the first pair of parentheses. If a match is found, whatever is matched can be accessed using $1. There are three pairs of parentheses in this expression. The first pair (starting from the left) is $1, the second one is $2, and the third one is $3. Notice that \ is used to escape the dot (.) metacharacter between the groups.

Here are two more examples:

+   • `^foo\.htm$`—This will match a string `foo.htm`. It would not match `afoo.htm` because the `^` metacharacter is used to specify that the matching string must start with the f character. It also would not match `foo.html` because the $ metacharacter is used to specify that the matching string must end with the m character.