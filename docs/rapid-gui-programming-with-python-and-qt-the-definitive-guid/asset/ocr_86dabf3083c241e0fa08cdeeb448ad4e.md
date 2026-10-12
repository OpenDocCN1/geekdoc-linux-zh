```
iconListWidget.setViewMode(QListView.IconMode)
```

Making the QTableWidget support drag and drop is achieved in exactly the same way, with a call of setAcceptDrops(True) and a call of setDragEnabled(True). No other code is necessary; what is shown is sufficient to allow users to drag icon and text items from one list widget to another, and to and from cells in the table.

The built-in drag-and-drop facilities are very convenient, and are often sufficient. But if we need to be able to handle our own custom data, we must reimplement some event handlers, as we will see in the following subsection.

# Handling Custom Data

The application shown in Figure 10.3 supports drag and drop for custom data; in particular, icons and text. (The source code is in chap10/customdraganddrop.pyw.) Although this is the same functionality as the built-in drag-and-drop facilities offer, the techniques used are generic and can be applied to any arbitrary data we like.

The icons and text can be dragged from the list widget on the left to the list widget on the right (which is in icon mode), or to the custom widget at the bottom left, or to the custom line edit at the bottom right—although in this last case only the text is used.

![](bbox=[0.26, 0.53, 0.74, 0.7])

For custom data that is put on the clipboard or used by PyQt's drag-and-drop system, we use QMimeType objects, with our own custom MIME types. MIME is a standardized format for handling multipart custom data. MIME data has a type and a subtype—for example, text/plain, text/html, or image/png. To handle custom MIME data we must choose a custom type and subtype, and wrap the data in a QMimeType object.

For this example we have created a MIME type of application/x/icon-and-text. It is good practice for custom MIME subtypes to begin with x-. We have stored the data in a QByteArray, a resizable array of bytes, and which for this example holds a QString and a QIcon, although it could hold any arbitrary data.