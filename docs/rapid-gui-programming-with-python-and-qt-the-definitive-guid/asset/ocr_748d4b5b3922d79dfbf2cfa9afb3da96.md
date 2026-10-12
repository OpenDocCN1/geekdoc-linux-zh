# 386  Chapter 13.  Rich Text and Printing

The event() handler is called before any of the specific key and mouse event handlers, and it is the only place where we can intercept and handle Tab key presses. If the user pressed Tab we get a QTextCursor from the QTextEdit; this allows us to programmatically interact with the underlying QTextDocument that holds the text. By default, the text cursor returned by a text edit is at the current insertion point (also called the cursor position), so we can simply insert four spaces. Then we return True to tell the event-handling system that we have handled the Tab key press and that no further action (such as changing focus) should take place.

To provide syntax highlighting we must create a QSyntaxHighlighter subclass, implement the highlightBlock() method, and create an instance of our highlighter with the QTextDocument we want it to apply to as an argument. We did the last part in the MainWindow's initializer, so now we will turn to our QSyntaxHighlighter subclass.

The QSyntaxHighlighter works on a line-by-line basis and provides a simple means of keeping track of state across multiple lines. For the Python Editor we will use regular expressions to identify the Python keywords, comments, and strings, including triple-quoted strings that span multiple lines, so that we can apply highlighting to them. We begin by setting up the regular expressions in the subclass's initializer, which we will look at in two parts.

```
```python
class PythonHighlighter(QSyntaxHighlighter):
    Rules = []
    def __init__ (self, parent=None):
        super(PythonHighlighter, self).__init__(parent)
        keywordFormat = QTextCharFormat()
        keywordFormat.setForeground(Qt.darkBlue)
        keywordFormat.setFontWeight(QFont.Bold)
        for pattern in (r"\b\w\d", r"\b\w", r"\b\w", ...):
            ... 
        PythonHighlighter.Rules.append((QRegExp(pattern), keywordFormat))
```
```

The Rules static list holds a list of pairs. The first element of each pair is a regular expression (a QRegExp) that is used to match a syntactic construct that can occupy only a single line (such as a Python keyword). The second element is a QTextCharFormat, an object that can hold information regarding how a piece of text should be formatted, such as its font and the pen that should be used to paint it.

We have created a rule for each Python keyword, giving each one the same keywordFormat format. (Most of the keywords are not shown in the snippet as indicated by the ellipsis.) Each keyword has a \b before and after it; this is a regular expression symbol that does not match any text, but rather matches at