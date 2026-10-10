# 8.9 Filters

A **filter** takes a stream of data from its standard input, transforms the data in some way, and sends the results to the standard output. Here are some of the filters commonly found on UNIX systems.

| Filter | Function |
| :--- | :--- |
| cat | Concatenate and display text |
| comm | Compare sorted files, selecting or rejecting lines common to both |
| crypt | Encode or decode text |
| cut | Cut out selected fields from input lines |
| diff | Display line-by-line differences between two files |
| egrep | Search text for a pattern using full regular expressions |
| fgrep | Search text for a character string |
| fmt | Format text |
| grep | Search a file for a pattern |
| head | Display the beginning (head) of a file |
| more | Show text, one screenful at a time |
| nl | Number lines |
| paste | Merge lines of text |
| pg | Show text, one screenful at a time |
| pr | Format and print text |
| sort | Sort and/or merge text |
| spell | Check for spelling errors |
| tail | Display last part of a file |
| tr | Translate characters |
| uniq | Display lines in a file that are unique |
| wc | Count number of lines, words, and characters in text |

Filters are often used with pipes and tee. Consider the **sort** utility, which, as you might expect, sorts its input. Suppose you wanted to list, alphabetically by their login names, the users currently logged onto your machine. You could do this by piping the output from **who** into **sort**:

```
`$ who | sort(Return)`
```

You can also give **sort** the name of a file to sort: