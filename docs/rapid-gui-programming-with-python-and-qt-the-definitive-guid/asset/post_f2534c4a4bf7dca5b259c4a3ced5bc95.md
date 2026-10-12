
![](img/9bfe0a027fcc8793bb087287001100dd_396_0.png)

Document, and it will be a useful widget in later chapters when we want to provide the ability for users to edit single lines of HTML text in database-type applications.

This chapter’s second section is devoted to printing. We have already seen how to print images and graphic scenes on a page, but in this section we will see how to print multiple page documents, including ones with embedded images. PyQt provides three different techniques for printing documents: one based on composing and printing HTML, another based on creating and printing QTextDocuments, and another based on using QPainter to paint directly onto the printer’s pages. We will show and discuss all three approaches.

## Rich Text Editing

In this section we will look at rich text editing from two different perspectives. In the first subsection we will create a plain text editor that uses QSyntaxHighlighter to provide syntax highlighting for Python source code. In the second subsection we will create a single-line rich text editor similar to QLineEdit, that has pop-up menus, and that supports various formatting shortcuts such as Ctrl+B and Ctrl+I to toggle bold and italic on and off. In both cases, we use QTextEdit as the foundation on which we build.

### Using QSyntaxHighlighter

If we want a Python-savvy text editor with syntax highlighting, we need not create one ourselves. The Tkinter-based IDLE application provides both a “sandbox” in which we can experiment with Python code, and a perfectly good Python code editor. And for more power, we can use Eric4, itself written in PyQt and using QScintilla for its text editing. However, no off-the-shelf editor will necessarily work in just the way we want, and since creating our own is instructive and revealing of what is involved, we will create a simple Python Editor to learn how to use QTextEdit and QSyntaxHighlighter. As the screenshot in Figure 13.1 shows, the Python Editor is a simple main-window-style application with two menus and toolbars. Since we have covered the creation of such applications before, we will focus just on those parts that are relevant to rich text editing, starting with the beginning of the main window’s initializer.

```python
class MainWindow(QMainWindow):
    def __init__(self, filename=None, parent=None):
        super(MainWindow, self).__init__(parent)

        font = QFont("Courier", 11)
        font.setFixedPitch(True)
        self.editor = QTextEdit()
        self.editor.setFont(font)

        self.highlighter = PythonHighlighter(self.editor.document())
        self.setCentralWidget(self.editor)
```

![](img/9bfe0a027fcc8793bb087287001100dd_397_0.png)

*Figure 13.1 The Python Editor editing itself*

We begin by creating a fixed-pitch font (a font where every character is the same width). Then we create a QTextEdit, a custom QTextEdit class that differs from QTextEdit in that it converts Tab key presses into insertions of four spaces. Next we create a PythonHighlighter, a QSyntaxHighlighter subclass, passing it the text editor's QTextDocument--this is the object in which the editor's text and formatting are actually stored. We make the editor the main window's central widget.

The rest of the initializer is concerned with the creation of the actions, menus, and toolbars, things that we are very familiar with and can therefore skip. The only other methods we will look at are two of the three basic file-handling ones, since they involve the text editor.

```python
def fileNew(self):
    if not self.okToContinue():
        return
    document = self.editor.document()
    document.clear()
    document.setModified(False)
    self.filename = None
    self.setWindowTitle("Python Editor - Unnamed")
    self.updateUi()
```

This method simply retrieves and clears the QTextDocument that actually holds the text, and sets the modified flag to False. The result is a blank QTextEdit with no unsaved changes. The updateUi() method is used to enable and disable actions depending on the application's state; see the Enabling and Disabling Actions sidebar on page 385.

```python
def loadFile(self):
    fh = None
    try:
        fh = QFile(self.filename)
        if not fh.open(QIODevice.ReadOnly):
            raise IOError, unicode(fh.errorString())
        stream = QTextStream(fh)
        stream.setCodec("UTF-8")
        self.editor.setPlainText(stream.readAll())
        self.editor.document().setModified(False)
        self.setWindowTitle("Python Editor – %s" % \
            QFileInfo(self.filename).fileName())
    except (IOError, OSError), e:
        QMessageBox.warning(self, "Python Editor — Load Error",
                            "Failed to load %s: %s" % (self.filename, e))
    finally:
        if fh is not None:
            fh.close()
```

If a file is loaded—for example, by the user invoking the File→Open action—this method is called. The file-handling code is similar to what we have seen before; the only real difference is that we set the QTextDocument's modified flag to False.

The code for saving (not shown) is very similar to that for loading. We get the file handle, create a QTextStream, set the encoding to UTF-8, and output the entire text using QTextEdit.toPlainText(). We also set the QTextDocument's modified flag to False.

```python
class TextEdit(QTextEdit):
    def __init__(self, parent=None):
        super(TextEdit, self).__init__(parent)

    def event(self, event):
        if event.type() == QEvent.KeyPress and \
           event.key() == Qt.Key_Tab:
            cursor = self.textCursor()
            cursor.insertText("    ")
            return True
        return QTextEdit.event(self, event)
```

The preceding code shows the complete TextEdit subclass. Every QTextDocument can be manipulated through a QTextCursor object, which is the programmatic equivalent of a user interacting with the document using key presses and mouse actions.

## Enabling and Disabling Actions

Sometimes particular actions are applicable only in certain circumstances. For example, it doesn't make much sense to allow "file save" on a document with no unsaved changes, or, arguably, to allow "file save as" on an empty document. Similarly, neither "edit copy" nor "edit py" makes sense if there is no selected text. One way to deal with this is to leave all the actions enabled all the time, but to make sure that they do nothing in cases where they don't make sense; for example, if we call QTextEdit.cut(), it will safely do nothing if there is no selected text.

Another solution is to enable and disable actions depending on the application's state. This can be achieved by doing three things: First, making actions that will be enabled and disabled into instance variables so that they can be accessed outside of the initializer; second, creating a method (e.g., updateUi()) that enables and disables actions depending on the application's state; and third, making application-specific signal-slot connections to updateUi() so that it is called whenever the application's state changes.

Using the Python Editor as an example, we need these connections:

```python
self.connect(self.editor,
    SIGNAL("selectionChanged()"), self.updateUi)
self.connect(self.editor.document(),
    SIGNAL("modificationChanged(bool)"), self.updateUi)
self.connect(QApplication.clipboard(),
    SIGNAL("dataChanged()"), self.updateUi)
```

These connections mean that if the editor's selection changes, or if the document is modified, or if the clipboard's data changes, we can enable or disable the relevant actions.

```python
def updateUi(self, arg=None):
    self.fileSaveAction.setEnabled(
        self.editor.document().isModified())
    self.fileSaveAsAction.setEnabled(
        not self.editor.document().isEmpty())
    enable = self.editor.textCursor().hasSelection()
    self.editCopyAction.setEnabled(enable)
    self.editCutAction.setEnabled(enable)
    self.editPasteAction.setEnabled(self.editor.canPaste())
```

This method is called in response to the signal-slot connections earlier. It is also called explicitly at the end of the initializer to set the user interface's initial state, and at the end of the fileView() method. The QTextEdit.canPaste() method was introduced with Qt 4.2; for earlier versions, use not QApplication.clipboard().text().isEmpty(). The text cursor and text document classes are covered later in this chapter.
