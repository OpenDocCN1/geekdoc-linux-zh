# ### Grouping expressions

Regular expression patterns can also be grouped by using parentheses. When you group a regular expression pattern, the group is treated like a standard character. You can apply a special character to the group just as you would to a regular character. For example:

```
`$ echo "Sat" | gawk '/Saturday|Sat/{print $0}'`
`Sat`
`$`
`$ echo "Saturday" | gawk '/Saturday|Sat/{print $0}'`
`Saturday`
`$`
```

The grouping of the “urday” ending along with the question mark allows the pattern to match either the full day name “Saturday” or the abbreviated name “Sat.”

It’s common to use grouping along with the pipe symbol to create groups of possible pattern matches:

```
`$ echo "cat" | gawk '/(c|b)a(b|t){print $0}'`
`cat`
`$`
`$ echo "cab" | gawk '/(c|b)a(b|t){print $0}'`
`cab`
`$`
`$ echo "bat" | gawk '/(c|b)a(b|t){print $0}'`
`bat`
`$`
`$ echo "bab" | gawk '/(c|b)a(b|t){print $0}'`
`bab`
`$`
`$ echo "tab" | gawk '/(c|b)a(b|t){print $0}'`
`$`
`$ echo "tac" | gawk '/(c|b)a(b|t){print $0}'`
`$`
```

The pattern (c|b)a(b|t) matches any combination of the letters in the first group along with any combination of the letters in the second group.

# ### Summary

If you manipulate data files in shell scripts, you need to become familiar with regular expressions. Regular expressions are implemented in Linux utilities, programming languages, and applications using regular expression engines. A host of different regular expression engines is available in the Linux world. The two most popular are the POSIX Basic Regular Expression (BRE) engine and the POSIX Extended Regular Expression (ERE) engine. `sed` conforms mainly to the BRE engine, whereas `gawk` utilizes most features found in the ERE engine.

A regular expression defines a pattern template that’s used to filter text in a data stream. The pattern consists of a combination of standard text characters and special characters. The special characters are used by the regular expression engine to match a series of one or more characters, similar to how wildcard characters work in other applications.