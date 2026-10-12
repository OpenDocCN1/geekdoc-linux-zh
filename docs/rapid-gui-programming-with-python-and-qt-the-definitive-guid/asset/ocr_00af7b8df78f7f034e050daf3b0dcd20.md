and so on recursively! To avoid this problem we set the text cursor to be at the last position in the document, which is the position following the last thing we inserted, that is, just after the table.

Finishing the page is simply a matter of inserting additional blocks with the appropriate formats, followed by inserting the relevant texts. For all pages except the last, we set the last block’s format to be lastParaBodyFormat, which (using Qt 4.2) will ensure that what follows will be on a fresh page.

```
document.print(self.printer)
```

The very last statement is where we print the document on the printer. At this point the document is complete, so we could call toHtml() on it to get it in HTML format if that was preferred. It also means that we can use a QTextCursor in conjunction with a QTextDocument to create HTML pages programmatically if we wanted.

The advantage of using QTextDocument, whether we give it an HTML string or whether we populate it using a QTextCursor, is that we can avoid doing lots of calculations to see where text should be placed on the page. The disadvantage is that PyQt puts page numbers on our documents whether we like them or not, and it does not give us fine positional control. Neither of these problems occurs if we use a QPainter.

# Printing Documents Using QPainter

We will conclude this section by looking at how to print using QPainter. Taking this approach means that we have the chore of doing all the position calculations ourselves, but also the benefit of being able to draw anything anywhere on the page, without being limited to what can be represented by HTML or by a QTextDocument. In addition, the painting itself uses the same methods and techniques that we have seen in the previous two chapters, since PyQt has a uniform approach to painting whether on widgets, on images, or on printed pages.

```
def printViaQPainter(self):
    dialog = QPrintDialog(self.printer, self)
    if not dialog.exec_():
        return

    LeftMargin = 72
    sansFont = QFont("Helvetica", 10)
    sansLineHeight = QFontMetrics(sansFont).height()
    serifFont = QFont("Times", 11)
    fm = QFontMetrics(serifFont)
    DateWidth = fm.width(" September 99, 2999 ")
    CreditWidth = fm.width(" Credit ")
    AmountWidth = fm.width(" W999999.99 ")
    serifLineHeight = fm.height()
```

![](bbox=[0.87, 0.17, 0.94, 0.23])