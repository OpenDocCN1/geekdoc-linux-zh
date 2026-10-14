Let’s try it:

```
[me@linuxbox ~]$ echo "This that" | grep -E '^([[:alpha:]]+ ?)+$'
This that
[me@linuxbox ~]$ echo "a b c" | grep -E '^([[:alpha:]]+ ?)+$'
a b c
[me@linuxbox ~]$ echo "a b 9" | grep -E '^([[:alpha:]]+ ?)+$'
[me@linuxbox ~]$ echo "abc d" | grep -E '^([[:alpha:]]+ ?)+$'
[me@linuxbox ~]$
```

We see that this expression does not match the line "a b 9", because it contains a non-alphabetic character; nor does it match "abc d", because more than one space character separates the characters c and d.

# { }—Match an Element a Specific Number of Times

The { and } metacharacters are used to express minimum and maximum numbers of required matches. They may be specified in four possible ways, as shown in Table 19-3.

# Table 19-3: Specifying the Number of Matches

| Specifier | Meaning |
|---|---|
| {n} | Match the preceding element if it occurs exactly n times. |
| {n,m} | Match the preceding element if it occurs at least n times, but no more than m times. |
| {n,} | Match the preceding element if it occurs n or more times. |
| {,m} | Match the preceding element if it occurs no more than m times. |

Going back to our earlier example with the phone numbers, we can use this method of specifying repetitions to simplify our original regular expression from

^(? [2-9][0-9][0-9]\ )? [0-9][0-9][0-9]-[0-9][0-9][0-9][0-9]$

to

^(? [0-9]{3})? [0-9]{3}-[0-9]{4}$

Let’s try it:

```
[me@linuxbox ~]$ echo "(555) 123-4567" | grep -E '^\(?[0-9]{3}\)? [0-9]{3}-[0-9]{4}$'
(555) 123-4567
[me@linuxbox ~]$ echo "555 123-4567" | grep -E '^\(?[0-9]{3}\)? [0-9]{3}-[0-9]{4}$'
555 123-4567
[me@linuxbox ~]$ echo "5555 123-4567" | grep -E '^\(?[0-9]{3}\)? [0-9]{3}-[0-9]{4}$'
[me@linuxbox ~]$
```