```
```text
[me@linuxbox ~]$ diff -c file1.txt file2.txt
*** file1.txt      2008-12-23 06:40:13.000000000 -0500
--- file2.txt      2008-12-23 06:40:34.000000000 -0500
***************
*** 1,4 ****
- a
  b
  c
  d
--- 1,4 ----
  b
  c
  d
+ e
```
```

The output begins with the names of the two files and their timestamps. The first file is marked with asterisks and the second file is marked with dashes. Throughout the remainder of the listing, these markers will signify their respective files. Next, we see groups of changes, including the default number of surrounding context lines. In the first group, we see:

`*** 1,4 ***`

which indicates lines one through four in the first file. Later we see:

`--- 1,4 ---`

which indicates lines one through four in the second file. Within a change group, lines begin with one of four indicators:

_Table 21-5: diff Context Format Change Indicators_

| Indicator | Meaning |
|---|---|
| `blank` | A line shown for context. It does not indicate a difference between the two files. |
| `-` | A line deleted. This line will appear in the first file but not in the second file. |
| `+` | A line added. This line will appear in the second file but not in the first file. |
| `!` | A line changed. The two versions of the line will be displayed, each in its respective section of the change group. |

The unified format is similar to the context format, but is more concise. It is specified with the `-u` option: