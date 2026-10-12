```
```cpp
pimid[0] = pop->insertItem( "Cut", this,
                  SLOT(doCut()) );
pimid[1] = pop->insertItem( "Copy", this,
                  SLOT(doCopy()) );
pmid[2] = pop->insertItem( "Paste", this,
                  SLOT(doPaste()) );
pmid[3] = pop->insertItem( "Clear All", this,
                  SLOT(doClear()) );
pop->insertSeparator();
pmid[4] = pop->insertItem( "Select All",
                  this, SLOT(doSelect()) );
pop->insertSeparator();
pmid[5] = pop->insertItem(
                  "Select All & Copy", this,
                  SLOT(doSelectCopy()) );
pmid[6] = pop->insertItem(
                  "Clear All & Paste", this,
                  SLOT(doClearPaste()) );
}

void
LineEdit::mousePressEvent( QMouseEvent *e )
{
    if(e->button() != RightButton) {
        QLineEdit::mousePressEvent( e );
        return;
    }
    int n = strlen(text());
    pop->setItemEnabled( pimid[0],
                    hasMarkedText() );
    pop->setItemEnabled( pimid[1],
                    hasMarkedText() );
    pop->setItemEnabled( pimid[3],
                    (n > 0) ? true : false );
    pop->popup( e->globalPos() );
}

void
LineEdit::doCopy()
{
    copy();
}

void
LineEdit::doCut()
{
    cut();
}

void
LineEdit::doPaste()
{
```
```