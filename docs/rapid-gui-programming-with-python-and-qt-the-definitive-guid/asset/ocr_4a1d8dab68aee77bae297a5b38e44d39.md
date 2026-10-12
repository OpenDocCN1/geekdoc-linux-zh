```
if what == RichTextLineEdit.Italic:
    self.toggleItalic()
return
if what == RichTextLineEdit.Underline:
    self.toggleUnderline()
return
```

Each text effect menu action had a constant stored in its user data; this constant is retrieved and held in the what variable. For the simple toggle actions, we only need to call the appropriate toggle method and we are finished.

```
format = self.currentCharFormat()
if what == RichTextLineEdit.Monospaced:
    format.setFontFamily(self.monofamily)
elif what == RichTextLineEdit.Serif:
    format.setFontFamily(self.seriffamily)
elif what == RichTextLineEdit.Sans:
    format.setFontFamily(self.sansfamily)
if what == RichTextLineEdit.StrikeOut:
    format.setFontStrikeOut(not format.fontStrikeOut())
if what == RichTextLineEdit.NoSuperOrSubscript:
    format.setVerticalAlignment(
        QTextCharFormat.AlignNormal)
elif what == RichTextLineEdit.Superscript:
    format.setVerticalAlignment(
        QTextCharFormat.AlignSuperScript)
elif what == RichTextLineEdit.Subscript:
    format.setVerticalAlignment(
        QTextCharFormat.AlignSubScript)
    self.mergeCurrentCharFormat(format)
```

To change the font family, strikeout format, or vertical alignment, we must retrieve the current formatting, apply the change that the user has asked for, and then merge the updated format with the current format to make it take effect.

We have now covered all the formatting options that the rich text line edit supports. Once the user has entered their rich text we will no doubt want to retrieve it so that we can store it, search it, or manipulate it. We could use the QTextEdit.toPlainText() method—but that will strip out all the HTML, leaving us no better off than if we had used a QLineEdit. A more suitable alternative is to use QTextEdit.toHtml(), but the HTML returned by this method is quite verbose since it must be general enough to cater for all the PyQt-supported HTML tags.

To put this in perspective, if we have the text “The **bold** cat.” (13 characters), where the word “bold” is in bold and the word “cat” is colored red, the toHtml() method returns 503 characters: