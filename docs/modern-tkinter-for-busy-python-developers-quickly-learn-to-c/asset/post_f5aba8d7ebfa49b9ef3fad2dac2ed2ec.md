
You can add text to a canvas using items of type “text”. You have complete control of the font, size, color and more, as well as the actual text that is displayed.

Perhaps most interestingly, you can embed other widgets (which would include a frame which itself contains other widgets) into a canvas using an item of type “window”. When we do this, the canvas in effect acts as a geometry manager for those other widgets. This capability raises all kinds of possibilities for your application.

There is a lot more to canvas widgets than we’ve described here; be sure to consult the reference manual, as well as the wide range of example programs included with the Tk distribution.

## Text

- Widget Roundup
- Reference Manual

A **text** widget manages a multi-line text area. Like the canvas widget, Tk’s text widget is an immensely flexible and powerful tool which can be used for a wide variety of tasks. Some example uses of text widgets have included anything from providing a simple multi-line text area as part of a form, to a stylized code editor, to an outliner, to a web browser. Text widgets are part of the classic Tk widgets, not the themed Tk widgets.

![](img/94378c1b05607c1dc5649c738af95c74_68_0.png)

Text widgets are created using the **Text** function:

```python
text = Text(parent, width=40, height=10)
```

While we briefly introduced text widgets in an earlier chapter, here we’ll go into much more detail, to give you a sense of the level of sophistication it allows. Still, for any significant work with the text widget, the reference manual is very well organized and useful.

### The Basics

If you just want to use the text widget to get a simple multi-line text from the user as part of a form, there’s only a few things you’ll need to worry about: creating and sizing the widget (check), providing an initial value for the text in the form, and retrieving the text in the widget after the user has submitted the form.

### Providing Initial Content

When you first create it, the text widget has nothing in it, so if you want to provide an initial piece of text, you’re going to have add it yourself. Unlike for example the entry widget, text widgets don’t support a “*textvariable*” configuration option; as we’ll soon see, text widgets can contain a lot more than just plain text, so a simple variable isn’t sufficient to hold it all.

Instead, to set the initial text for the widget, you’ll use the widget’s “*insert*” method:

```python
text.insert("1.0", "here is my text to insert")
```

The "1.0" here represents where to insert the text, and can be read as "line 1, character 0". This refers to the first character of the first line; for historical conventions related to how programmers normally refer to lines and characters, line numbers are 1-based, and character numbers are 0-based.

The text to insert is just a string. Because the widget can hold multi-line text, the string you supply can be multi-line as well. To do, simply embed "\n" (newline) characters in your string at the appropriate locations.

### Scrolling

Scrollbars, both horizontal and vertical, can be attached to the text widget. This works exactly the same as using scrollbars in any other widget, such as a listbox or canvas.

You can also ask the widget to ensure that a certain part of the text is visible. For example, if you've added more text to the widget than will fit onscreen (so it will scroll) but want to ensure that the top of the text rather than the bottom is visible, call the "see" method, passing it the position of the text (e.g., "1.0").

### Controlling Wrapping

What if some lines of text in the widget are very long, longer than the width of the widget? By default, text will just wrap around to the next line, but if and how it does this can be controlled by the "wrap" configuration option. The default value is "char", meaning wrap around right at the character at the end of the line; other options are "word" to cause wrapping, but only at word breaks (e.g. spaces), and "none" meaning don't wrap around at all. In the latter case, some of the text won't be visible unless you attach a horizontal scrollbar to the widget.

### Disabling the Widget

Some forms will temporarily disable editing in particular widgets unless certain conditions are met (e.g. some other options are set to a certain value). To prevent the user from making any changes to a text widget, set the "state" configuration option to "disabled"; re-enable editing by setting this option back to "normal".

### Retrieving the Text

Finally, after the user has made any changes and submitted the form, your program will want to retrieve the contents of the widget, which is done with the "get" method:

```python
texttext = text.get('1.0', 'end')
```

### Modifying the Text in Code

While the user can modify the text in the text widget interactively, your program can also make changes. Adding text is done with the "insert" method, which we used above to provide an initial value for the text widget.

### Text Positions and Indices

When we specified a position of "1.0" (first line, first character), this was an example of an index. It tells the insert method where to insert the new text (just before the first line, first character, i.e. at the very start of the widget). There are a variety of ways to specify these indices. You've also seen another one: the "end" (from the "get" example) means just past the end of the text ("just past" because text insertions go right before the given index, so inserting at "end" will add text to the end of the widget). Note that Tk will always add a newline at the very end of the text widget.

Here are a few additional examples of indices, and what they mean:

- `3.end`: The newline at the end of line 3.
- `1.0 + 3 chars`: Three characters past the start of line 1.
- `2.end - 1 chars`: The last character before the new line in line 2.
- `end - 1 chars`: The newline that Tk always adds at the end of the text.
- `end - 2 chars`: The actual last character of the text.
- `end - 1 lines`: The start of the last actual line of text.
- `2.2 + 2 lines`: The third character (index 2) of the fourth line of text.
- `2.5 linestart`: The first character of line 2.
- `2.5 lineend`: The position of the newline at the end of line 2.
- `2.5 wordstart`: The first character of the word containing the character at index 2.5.
- `2.5 wordend`: The first character just past the last character of the word containing index 2.5.

Some additional things to keep in mind:

- The term "chars" can be abbreviated as "c", and "lines" as "l".
- You can omit the spaces between the terms, e.g. "1.0+1c".
- If you specify an index past the end of the widget (e.g. "end + 100c") it will be interpreted as the end.
- Adding characters will wrap to the next lines as needed, e.g. "1.0 + 10 chars" on a line with only five characters will end up being on the second line.
- When using indices containing multiple words, make sure to quote them appropriately so that Tk sees the entire index as a single argument.
- When moving up or down a certain number of lines, this is interpreted as logical lines, where each line is terminated only by the "\n". With long lines and wrapping enabled, this may be represent multiple lines on the display. If you'd like to move up or down a single line on the display, you can specify this as e.g. "1.0 + 2 display lines".
- To determine the actual canonical position of an index, use the "index" method, passing it the index expression, and it will return the corresponding index in the form "line.char".
- You can compare two indices using the "compare" method, which lets you check for equality, whether one index is later in the text than the other, etc.

### Deleting Text

While the "insert" method adds new text anywhere in the widget, the "delete" method removes it. You can specify either a single character to be deleted (by index), or a range of characters specified by the start and end index. In the latter case, characters from (and including) the start index through to just before the end index will be deleted (so the character at the end index is not deleted). So this would remove a single line of text (including its trailing newline) from the start of the text:

```python
text.delete('1.0', '2.0')
```

There is also a "replace" method, taking a starting index, and ending index and a string as parameters. It does the same as a delete, followed by an insert at the same location.

### Example: Logging Window

Here's a short example illustrating how to use a text widget as a 80x24 logging window for your application. The user doesn't edit the text widget at all; instead, your program will write log messages to it. You'd like to keep the content to no more than 24 lines (so no scrolling), so as you add new messages at the end, you'll have to remove old ones from the top if there are already 24 lines.

```python
from tkinter import *
from tkinter import ttk

root = Tk()
log = Text(root, state='disabled', width=80, height=24, wrap='none')
log.grid()

def writeToLog(msg):
  numlines = log.index('end - 1 line').split('.')[0]
  log['state'] = 'normal'
  if numlines == 24:
    log.delete('1.0', '2.0')
  if log.index('end-1c') != '1.0':
    log.insert('end', '\n')
```
