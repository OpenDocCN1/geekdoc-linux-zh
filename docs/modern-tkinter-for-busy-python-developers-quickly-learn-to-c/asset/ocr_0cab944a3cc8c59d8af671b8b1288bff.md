end -1 lines The start of the last actual line of text.
2.2 + 2 lines The third character (index 2) of the fourth line of text.
2.5 linestart The first character of line 2.
2.5 lineend The position of the newline at the end of line 2.
2.5 wordstart The first character of the word containing the character at index 2.5.
2.5 wordend The first character just past the last character of the word containing index 2.5.

Some additional things to keep in mind:
•The term "chars" can be abbreviated as "c", and "lines" as "l".
•You can omit the spaces between the terms, e.g. "1.0+1c".
•If you specify an index past the end of the widget (e.g. "end + 100c") it will be interpreted as the end.
•Adding characters will wrap to the next lines as needed, e.g. "1.0 + 10 chars" on a line with only five characters will end up being on the second line.
•When using indices containing multiple words, make sure to quote them appropriately so that Tk sees the entire index as a single argument.
•When moving up or down a certain number of lines, this is interpreted as logical lines, where each line is terminated only by the "\n". With long lines and wrapping enabled, this may be represent multiple lines on the display. If you'd like to move up or down a single line on the display, you can specify this as e.g. "1.0 + 2 display lines".
•To determine the actual canonical position of an index, use the "index" method, passing it the index expression, and it will return the corresponding index in the form "line.char".
•You can compare two indices using the "compare" method, which lets you check for equality, whether one index is later in the text than the other, etc.

# Deleting Text

While the "insert" method adds new text anywhere in the widget, the "delete" method removes it. You can specify either a single character to be deleted (by index), or a range of characters specified by the start and end index. In the latter case, characters from (and including) the start index through to just before the end index will be deleted (so the character at the end index is not deleted). So this would remove a single line of text (including its trailing newline) from the start of the text:
text.delete('1.0', '2.0')

There is also a "replace" method, taking a starting index, and ending index and a string as parameters. It does the same as a delete, followed by an insert at the same location.

# Example: Logging Window

Here's a short example illustrating how to use a text widget as a 80x24 logging window for your application. The user doesn't edit the text widget at all; instead, your program will write log messages to it. You'd like to keep the content to no more than 24 lines (so no scrolling), so as you add new messages at the end, you'll have to remove old ones from the top if there are already 24 lines.

```
```python
from tkinter import *
from tkinter import ttk

root = Tk()
log = Text(root, state='disabled', width=80, height=24, wrap='none')
log.grid()

def writeToLog(msg):
  numlines = log.index('end - 1 line').split('.')[0]
  log['state'] = 'normal'
  if numlines==24:
    log.delete(1.0, 2.0)
  if log.index('end-1c')!=1.0':
    log.insert('end', '\n')
```
```