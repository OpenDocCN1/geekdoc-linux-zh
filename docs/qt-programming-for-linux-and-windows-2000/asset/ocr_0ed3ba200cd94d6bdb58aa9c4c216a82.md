```
```
paste();
}

void
LineEdit::doSelect()
{
    selectAll();
}

void
LineEdit::doClear()
{
    setText( "" );
}

void
LineEdit::doClearPaste()
{
    setText( "" );
    paste();
}

void
LineEdit::doSelectCopy()
{
    selectAll();
    copy();
}

#include <LineEdit.moc>
```
```

Lineedit.cpp

This final modification provides for selecting and highlighting existing contents of a QLineEdit widget whenever the widget obtains keyboard focus:

```
```
LineEdit.h
#ifndef LINEEDIT_H
#define LINEEDIT_H
#include <qevent.h>
#include <qlineedit.h>

class LineEdit : public QLineEdit
{
    Q_OBJECT
public:
    LineEdit( QWidget *parent=0,
        const char *name=0 );

protected slots:
    void    focusInEvent( QFocusEvent * );
```
```