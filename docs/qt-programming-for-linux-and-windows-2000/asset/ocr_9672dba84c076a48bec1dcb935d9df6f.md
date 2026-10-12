The following example produces the dialog displayed in Figure 3.10:

# *Example Use*

```
```
bool retry = FALSE;
QString svr = QInputDialog::getText( "Enter Hostname",
      "Hostname or IP Address:",
      "ftp.kahuna-surf.org",
      &retry, this );
if( retry == true && !svr.isEmpty() )
    // Deal with a retry attempt
else
    // No hostname or user pressed cancel
```
```

# QMessageBox

This is the standard message box widget for Qt. It consists of a dialog box, an optional icon, a dialog caption, a label for some text, and up to three buttons with customizable labels.

![](bbox=[0.08, 0.52, 0.7, 0.65])

It provides the usual warning() (see Fig. 3.11 for an example), critical(), and information() methods that determine the icon displayed with the message box text that you supply and they're very simple to use:

# *Example Use*

```
```
QMessageBox::information( this, "Info", "Details" );
```
```

# QProgressDialog

A QProgressDialog (Fig 3.12) provides progress feedback to the end-user. (See Fig. 3.12.)You may want to implement these for operations that take a long time to complete.