actions depending on the application's state; see the Enabling and Disabling Actions sidebar on page 385.

```
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
        self.setWindowTitle("Python Editor – %s" % \\
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

```
class TextEdit(QTextEdit):
    def __init__(self, parent=None):
        super(TextEdit, self).__init__(parent)

    def event(self, event):
        if event.type() == QEvent.KeyPress and \\
           event.key() == Qt.Key_Tab:
            cursor = self.textCursor()
            cursor.insertText("   ")
            return True
        return QTextEdit.event(self, event)
```

The preceding code shows the complete TextEdit subclass. Every QTextDocument can be manipulated through a QTextCursor object, which is the programmatic equivalent of a user interacting with the document using key presses and mouse actions.