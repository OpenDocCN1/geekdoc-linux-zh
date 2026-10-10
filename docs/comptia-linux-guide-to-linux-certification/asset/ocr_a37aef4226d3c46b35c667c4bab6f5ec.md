| Regular Expression | Description | Example | Type |
| --- | --- | --- | --- |
| `*` | Matches 0 or more occurrences of the previous character | `letter*` matches lette, letter, letterr, leterrrr, and so on | Common |
| `?` | Matches 0 or 1 occurren ces of the previous character | `letter?` matches lette, letter | Extended |
| `+` | Matches 1 or more occurrences of the previous character | `letter+` matches let, letterr, leterrrr, and so on | Extended |
| `. (period)` | Matches 1 character of any type | `letter.` matches lettere, letterb, letterc, letter1, letter2, letter3, and so on | Common |
| `[^...]` | Matches one character NOT from the range specified within the braces | `letter[^1238]` matches letter4, letter5, letter6, letter8;`letter[^-c]` matches lettere, letterb, and letter | Common |
| `{ }` | Matches a specific number or range of the previous character | `letter{3}` matches letter1, leter2, whereas letter {2,4} matches letterr, leterrr, and leterrrr | Extended |
| `^` | Matches the following characters if they are the first characters on the line | `^letter` matches letter if letter is the first set of characters in the line | Common |
| `$` | Matches the previous characters if they are the last characters on the line | `letter$` matches letter if letter is the last set of characters in the line | Common |
| `(... \| ...)` | Matches either of two sets of characters | `(mother\|father)` matches the word "mother" or "father" | Extended |

# **Table 3-4** Regular expressions

The `grep` command requires two arguments at minimum, the first argument specifies which text to search for, and the remaining arguments specify the files to search. If a pattern of text is matched, the `grep` command displays the entire line on the terminal screen. For example, to list only those lines in the file `project4` that contain the words “Algonquin Park,” enter the following command:

```
[root@server1 ~]# grep "Algonquin Park" project4
room this year while vacationing in Algonquin Park - I
I have been reading on the history of Algonquin Park but
[root@server1 ~]#_
```

To return the lines that do not contain the text “Algonquin Park,” you can use the `-v` option of the `grep` command to reverse the meaning of the previous command:

```
[root@server1 ~]# grep -v "Algonquin Park" project4
Hi there, I hope this day finds you well.
Unfortunately we were not able to make it to your din ing
especially wished to see the model of the Highland Inn
and the train station in the dining room.
```