# Table 11.8 Regular Expression Wildcards (continued)

| Regular Expression | Meaning |
|---|---|
| no!(thing|where) | ! matches all strings except those matched by any of the patterns in the parentheses. Matches no, nobody, or none, but not nothing or nowhere. |

# EXAMPLE 11.32

```
1  $ ls
abc abc1 abc122 abc123 abc2 file1 file1.bak file2 file2.bak none
nonsense none none nothing nowhere one
2  $ ls abc{1|2}
abc abc1 abc2
3  $ ls abc{([1-5])}
abc abc1 abc122 abc123 abc2
4  $ ls abc+([1-5])
abc1 abc122 abc123 abc2
5  $ ls no@(thing|ne)
none nothing
6  $ ls no!(one|nonsense)
none nothing nowhere
```

# EXPLANATION

+   1 All the files in the present working directory are listed.
+   2 Matches filenames starting with abc and followed by zero characters or one of either of the patterns in parentheses. Matches abc, abc1, or abc2.
+   3 Matches filenames starting with abc and followed by zero or more numbers between 1 and 5. Matches abc, abc1, abc122, abc123, and abc2.
+   4 Matches filenames starting with abc and followed by one or more numbers between 1 and 5. Matches abc1, abc122, abc123, and abc2.
+   5 Matches filenames starting with no and followed by exactly thing or ne. Matches nothing or none.
+   6 Matches filenames starting with no and followed by anything except one or nonsense. Matches none, nothing, and nowhere.

# 11.8.7 The noglob Variable

If the noglob variable is set, filename substitution is turned off, meaning that all metacharacters represent themselves; they are not used as wildcards. This can be useful when searching for patterns containing metacharacters in programs like grep, sed, or awk. If noglob is not set, all metacharacters must be escaped with a backslash if they are not to be interpreted.