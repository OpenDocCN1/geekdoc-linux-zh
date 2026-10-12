search, and emit a signal with the position in the text where the find text
was found.

```
    def makeRegex(self):
        findText = unicode(self.findLineEdit.text())
        if unicode(self.syntaxComboBox.currentText()) == "Literal":
            findText = re.escape(findText)
        flags = re.MULTILINE|re.DOTALL|re.UNICODE
        if not self.caseCheckBox.isChecked():
            flags |= re.IGNORECASE
        if self.wholeCheckBox.isChecked():
            findText = r'\b%s\b' % findText
        return re.compile(findText, flags)
```

We begin with getting the find text that the user has entered. We know that it
cannot be empty because the buttons (apart from the Close button) are enabled
only if there is some find text. If the user has chosen a literal text search, we
use the re.escape() function to escape any regular expression meta-characters
(like "\\") that may be in the user's find text. Then we initialize our search
flags. We supplement the flags with the re.IGNORECASE flag if the caseCheckBox is
unchecked. If the user has asked to search for whole words, we put a \b before
and after the find text: This is a token in Python's (and QRegExp's) regular ex-
pression language that specifies a word boundary. The r in front of the string
literal indicates a "raw" string in which we can write characters like "\\" un-
escaped. Finally we return the regular expression in compiled (ready-to-use)
form.*

> Raw
> strings
> 157'§a

If we knew that the text to be searched was normally going to be a QString
rather than a unicode, it might be preferable to use the PyQt's QRegExp class
rather than the Python standard library's re class.

```
    @pyqtSignature("")
    def on_replaceButton_clicked(self):
        regex = self.makeRegex()
        self.__text = regex.sub(unicode(self.replaceLineEdit.text()),
                                self.__text, 1)
```

This method is quite simple because it passes on its preparation work to the
makeRegex() method. We use the sub method ("substitute") to replace the first
occurrence of the find text with the replacement text. The replacement text
could be empty. The 1 is the maximum number of replacements to make.

```
    @pyqtSignature("")
    def on_replaceAllButton_clicked(self):
        regex = self.makeRegex()
```

> *The QRegExp documentation provides a brief introduction to regular expressions. Python's regular
> expression engine is covered in the re module documentation. For in-depth coverage see Mastering
> Regular Expressions by Jeffrey E. Friedl.