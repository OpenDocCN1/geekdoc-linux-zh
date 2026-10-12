movie’s title in the first cell (item) of each row, and set this item’s user data to hold the movie’s id(). We must convert the ID to be a long, to ensure that it is held correctly inside the QVariant. Once the item has been created and set up, we put it in the table at the appropriate row and column.

We only populate the year and minutes cells if we have data for them. For the notes, we truncate and add an ellipsis if the data is long, since notes could be many paragraphs in size.

```
self.table.resizeColumnsToContents()
if selected is not None:
    selected.setSelected(True)
    self.table.setCurrentItem(selected)
    self.table.scrollToItem(selected)
```

Once all the table items have been added, we resize the table’s columns to match their contents.

When we iterate over the movies in the movie container, the movies are returned in alphabetical order (but ignoring leading “A”, “An”, and “The”, words). If the user adds a new movie or edits an existing movie, we want to ensure that the movie they have just added or edited is both selected and visible. This is achieved by calling updateTable() after the add or edit, with the ID of the movie they added or edited. At the end of updateTable(), if a movie ID was passed in, the selected variable will hold the item corresponding to the movie’s title cell, and this item (and therefore the item’s row) will be made both current and selected, and if necessary the table widget will scroll to make sure that the row is visible to the user.

```
def fileNew(self):
    if not self.okToContinue():
        return
    self.movies.clear()
    self.statusBar().clearMessage()
    self.updateTable()
```

This method is similar to the method of the same name used for the Image Changer application. The key difference is that instead of the main window being responsible for the data, the work is delegated to the movie container held in self.movies. When updateTable() is called, there will be no movie records, so the widget will just show the column headers and nothing else.

The okToContinue() method is almost the same as the one we used in the Image Changer application. The only difference is that instead of the condition checking self.dirty (since the Image Changer’s main window held the application’s data) it calls self.movies.isDirty() because in this application, the movies container holds the data.

```
def fileOpen(self):
    if not self.okToContinue():
```