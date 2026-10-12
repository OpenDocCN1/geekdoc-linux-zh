Using our help form is easy: We just give it one of the HTML files, and self (over which the form will center itself). Notice that we use show() rather than exec( ); this almost always means that the form shown will have the delete on close attribute set.

The screenshot in Figure 17.1 may give the misleading impression that keyboard users are not catered to, but in fact, the class used to show the HTML files, QTextBrowser, provides good keyboard support. For example, users can press Tab to move the focus from hyperlink to hyperlink, and Enter to follow a hyperlink. They can go back by pressing Alt+Left Arrow, and they can go to the first page by pressing Home. And because the form is a QDialog subclass, they can close the window by pressing Esc.

By now we are very familiar with creating PyQt dialogs, so we will confine ourselves to showing just those extracts that are relevant to creating the online help system—specifically, a couple of extracts from the HelpForm's initializer, and one of its methods. (The code is in chap17/helpform.py.)

```
class HelpForm(QDialog):

    def __init__(self, page, parent=None):
        super(HelpForm, self).__init__(parent)
        self.setAttribute(Qt.WA_DeleteOnClose)
        self.setAttribute(Qt.WA_GroupLeader)
```

The Qt.WA_GroupLeader attribute ensures that if the help form is invoked from a modal dialog, the user will be able to interact with both the modal dialog and the help form, something that would not be possible otherwise. If the help form is invoked from a modeless dialog or main window, the attribute has no effect, and the user can interact with both as usual.

```
self.textBrowser.setSearchPaths([":/"])
self.textBrowser.setSource(QUrl())
```

The QTextBrowser class is a subclass of QTextEdit that can be used to display a large subset of HTML tags, including images, lists, and tables. We have set its search path to the resource file's root directory, and set its initial page to be the page that was passed in. Because we have set a search path we are able to pass a page without a path (e.g., simply index.html or filemenu.html). The QTextBrowser understands resource paths, and is therefore able to find image resources in `<img>` tags such as `<img src=":/filenew.png">`.

```
self.connect(backAction, SIGNAL("triggered()"),
            self.textBrowser, SLOT("backward()"))
self.connect(homeAction, SIGNAL("triggered()"),
            self.textBrowser, SLOT("home()"))
self.connect(self.textBrowser, SIGNAL("sourceChanged(Qurl)"),
            self.updatePageTitle)
```