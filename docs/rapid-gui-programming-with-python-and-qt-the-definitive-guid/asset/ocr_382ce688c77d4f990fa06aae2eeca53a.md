```
return
path = QFileInfo(self.movies.filename()).path() \\
if not self.movies.filename().isEmpty() else "."
fname = QFileDialog.getOpenFileName(self,
"My Movies - Load Movie Data", path,
"My Movies data files (%s)" %
self.movies.formats())
if not fname.isEmpty():
ok, msg = self.movies.Load(fname)
self.statusBar().showMessage(msg, 5000)
self.updateTable()
```

The file open method is structurally the same as we have seen before. The movie container holds the current filename as a QString. Normally, an application has just one custom file format, but for the sake of illustration the My Movies application supports several, so we have provided a formats() method to return the extensions that can be used.

The main window subclass passes on the work of loading to the movies container. We have designed our movie container’s load and save methods to return a Boolean success/failure flag and a message. The message is either an error message, or a report of how many movie records were loaded or saved. In the My Movies application, we use only the message.

If the load is successful, the movie container will contain the new movie records and updateTable() will display them. If the load failed, the movie container will be empty, and updateTable() will show only the column headers.

```
def fileSave(self):
if self.movies.filename().isEmpty():
self.fileSaveAs()
else:
ok, msg = self.movies.save()
self.statusBar().showMessage(msg, 5000)
```

Again, the logic for this method is the same as we have seen before. The code used for saving and loading depends on the filename extension, as we will see later.

We will skip the code for fileSaveAs(); it is the same as for the Image Changer application, except that we use Qstring rather than unicode methods with the filename, and we use a default extension of .mgb (My Movies in Qt binary format).

```
def fileImportDOM(self):
self.fileImport("dom")

def fileImportSAX(self):
self.fileImport("sax")
```