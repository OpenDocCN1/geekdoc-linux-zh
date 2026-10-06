# !string Event Text

When a string of text follows an exclamation point, the shell searches for and executes the most recent event that *began* with question marks, If you enclose the string, the shell executes the most recent event that *contained* that string. The final question mark is optional if a RETURN would immediately follow it:

```
68 $ history
59 ls -l text* 60 tail text5
61 cat text1 > letter
62 vi letter
63 cat letter
64 cat memo
65 l1 memo
66 pine jenny
67 ls -l
68 $ history
69 $ !
1s -l
```

```
70 $ !lp
1p memo
request id is printer_1-1016 (1 file)
71 $ !?letter?
cat letter
```

# Optional

# !n:w Word within an Event

You can select any word or series of words from an event. The words are numbered starting with 0, representing the first word (usually the command) on the line, and continuing with 1, representing the first word following the command, through n, representing the last word on the line.

To specify a particular word from a previous event, follow the event designator (such as !14) with a colon and the number of the word in the previous event (for example, use !14:3 to specify the third word following the command from event 14). You can specify a range of words by separating two word designators with a hyphen. The first word following the command (word number 1) can be specified by a caret (^) and the last word by a dollar sign ($):