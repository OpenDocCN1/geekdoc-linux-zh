input stream. The simplest form of address is a line number. We can add one to our example.

```
[me@linuxbox ~]$ echo "front" | sed '1s/front/back/'
back
```

Adding the address 1 to our command causes our substitution to be performed on the first line of our one-line input stream. If we specify another number, we see that the editing is not carried out since our input stream does not have a line 2.

```
[me@linuxbox ~]$ echo "front" | sed '2s/front/back/'
front
```

Addresses may be expressed in many ways. Table 20-7 lists the most common.

# Table 20-7: sed Address Notation

| Address | Description |
|---|---|
| n | A line number where n is a positive integer. |
| $ | The last line. |
| /regexp/ | Lines matching a POSIX basic regular expression. Note that the regular expression is delimited by slash characters. Optionally, the regular expression may be delimited by an alternate character, by specifying the expression with \cregexpc, where c is the alternate character. |
| addr1,addr2 | A range of lines from addr1 to addr2, inclusive. Addresses may be any of the single address forms listed earlier. |
| first~step | Match the line represented by the number first and then each subsequent line at step intervals. For example, 1~2 refers to each odd numbered line, and 5~5 refers to the fifth line and every fifth line thereafter. |
| addr1,+n | Match addr1 and the following n lines. |