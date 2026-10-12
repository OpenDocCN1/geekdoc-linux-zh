# QFileDialog

QFileDialogs (see Fig. 3.8) are used to allow an end-user to select a file for open or save functionality, or to select or create a subdirectory.

![](bbox=[0.12, 0.15, 0.88, 0.46])

Figure 3.8  QFileDialog widget

This is another static dialog, so it will typically be used in the following manner:

# Example Use

```
// Get a filename from the user to save to
QString s = QFileDialog::getSaveFileName( "*.txt" );
if(!s.isNull()) { // Save it
…
} // else user cancelled
…
```

# QFontDialog

The font dialog (see Fig. 3.9) is used to prompt the user for a text font and typeface. As is the case with most Qt dialogs, QFontDialog has no constructor. A typical use goes something like:

# Example Use

```
…
bool ret;
QLabel *l = new QLabel( "Altered Font", this );
QFont f = QFontDialog::getFont( &ret, this );
```