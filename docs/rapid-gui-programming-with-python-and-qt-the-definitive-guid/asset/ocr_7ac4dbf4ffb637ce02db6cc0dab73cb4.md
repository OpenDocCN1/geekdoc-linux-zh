```
```
if balance < 0:
    painter.setPen(Qt.red)
    text = "Please remit the amount owing immediately."
else:
    text = ("We are delighted to have done business "
            "with you.")
    painter.drawText(x, y, text)
```
```

After the addresses we print the form letter with its text depending on the state of the account as usual.

```
```
painter.setPen(Qt.black)
y += int(serifLineHeight * 1.5)
painter.drawText(x, y, "Transactions:")
y += serifLineHeight
option = QTextOption(Qt.AlignRight | Qt.AlignVCenter)
```
```

For the table of transactions we begin by writing the table's title and then we create a QTextOption object. These objects can be used to specify a variety of text-formatting options, including alignment and word wrapping.

```
```
for date, amount in statement.transactions:
    x = LeftMargin
    h = int(fm.height() * 1.3)
    painter.drawRect(x, y, DateWidth, h)
    painter.drawText(
        QRect(x + 3, y + 3, DateWidth - 6, h - 6),
        date.toString(DateFormat), option)
    x += DateWidth
    painter.drawRect(x, y, CreditWidth, h)
    text = "Credit"
    if amount < 0:
        text = "Debit"
    painter.drawText(
        QRect(x + 3, y + 3, CreditWidth - 6, h - 6),
        text, option)
    x += CreditWidth
    painter.drawRect(x, y, AmountWidth, h)
    if amount < 0:
        painter.setPen(Qt.red)
    painter.drawText(
        QRect(x + 3, y + 3, AmountWidth - 6, h - 6),
        QString("% %L1").arg(float(amount), 0, "f", 2),
        option)
    painter.setPen(Qt.black)
    y += h
```
```