Qt list boxes use QListBoxItems for displayed content. This is a little different from other toolkits' implementations, but provides much greater flexibility in controlling the contents of the list.

# QListBoxItem

This is the base class for all QListBox line items. It is subclassed by QListBoxPixmap and QListBoxText, which are discussed below.

While it is certainly a matter of preferences and style, I feel it is confusing to provide multiple objects in a list item (e.g., a pixmap and a text item). This is only because a listbox does not provide column headers that provide a clue as to what the user is supposed to be looking at. Aren't opinions useful?

# QListBoxPixmap

This is a list box item that provides only a pixmap.

# QListBoxText

This is a list box item that provides only a text label.

# QListView

List views (Fig 3.19) provide a tabular view with optional tree behavior. List views display QListViewItems, which can contain a limited number of pixmap or text label items. The Qt examples included with the Qt software distribution adequately demonstrate the many uses for list views, so I won't bore you with detailed examples.

![](bbox=[0.13, 0.48, 0.88, 0.7])

# A Possible Instantiation

```
QListView *theView = new QListView( this );
```

# Example Use

```
// Create a list and implied header-3 cells
QListView *theView = new QListView( this );
```