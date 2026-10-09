*!string* event text When a string of text follows an exclamation point, the shell searches for and executes the most recent event that *began* with that string. If you enclose the string within question marks, the shell executes the most recent event that *contained* that string. The final question mark is optional if a RETURN would immediately follow it.

```
```
68 $ history 10
59  ls -l  text*
60  tail text5
61  cat text1 text5 > letter
62  vim.tiny letter
63  cat letter
64  cat memo
65  lpr memo
66  pine zach
67  ls -l
68  history
69 $ !l
ls -l
...
70 $ !lpr
lpr memo
71 $ !?letter?
cat letter
...
```
```

Table 9-8 Event Designators
| Designator | Meaning |
| :--- | :--- |
| `!` | Starts a history event unless followed immediately by SPACE, NEWLINE, =, or (. |
| `!!` | The previous command. |
| `!n` | Command number *n* in the history list. |
| `!-n` | The *nth* preceding command. |
| `!string` | The most recent command line that started with *string*. |
| `!?string[?]` | The most recent command that contained *string*. The last ? is optional. |
| `!#` | The current command (as you have it typed so far). |
| `!(event)` | The *event* is an event designator. The braces isolate *event* from the surrounding text. For example, `!(3)` is the third most recently executed command followed by a 3. |


# Optional Word Designators

A *word designator* specifies a word (token) or series of words from an event. (Table 9-9 on page 338 lists word designators.) The words are numbered starting with 0 (the first word on the line—usually the command), continuing with 1 (the first word following the command), and ending with *n* (the last word on the line).