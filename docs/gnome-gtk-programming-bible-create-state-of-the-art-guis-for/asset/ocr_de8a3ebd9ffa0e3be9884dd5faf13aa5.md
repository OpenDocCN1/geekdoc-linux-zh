The function makeBox() beginning on line 150 uses boxes to construct the layout. A horizontal box is used to hold the two buttons, and a vertical box is used to hold the label and the horizontal box. Each button is assigned a callback function—the “Previous” button calls previous() and the “Next” button calls next().

The callback function next() beginning on line 125 increments the cursor index value by one—if it is not already at the end of the array. The count of the number of members in the array is calculated by dividing the size of the entire array by the size of one member. The callback function previous() reduces the index by one if the index is larger than zero. In both functions, if the index value is incremented, a call is made to setCursor() to change the current cursor.

The setCursor() function beginning on line 140 changes the current cursor to the one in the array addressed by the index. If a cursor is already created, it is destroyed before a new one is created. If your program uses several cursors, you can create them once and reuse them as needed. A call is made to gdk_cursor_new() to create a GdkCursor object. Using this new cursor in a call to gtk_label_set_cursor() makes the new cursor become the one used by the top-level window and its descendants. (The cursor is also changed for the buttons and the label.) Finally, the text of the label is updated by a call to gtk_label_set_text() so the name of the cursor is displayed.

![](bbox=[0.14, 0.49, 0.21, 0.56])

> **Note**
> The built-in cursors are all defined by the list of named values in the file gtk/gdk/gdkcursors.h, which is included by gtk/gdk/gtkcursors.h where it is used as the body of an enum. The list of cursors is quite stable—most of them have been a part of X for several years. However, it is possible that some new entries will be made and, if so, you will need to update the list of names and values compiled into this program.

# Create Cursor

It is a simple matter to create your own cursor. The bitmap utility can be used to create both the cursor and the mask to go with it. Then, these two bitmaps can be converted directly into the current cursor.

A cursor is normally black and white. It either has a black body with white trim surrounding it, or it has a white body with black trim. This way, the cursor can be placed on top of any color (including black or white) and still be visible. Also, cursors usually are kept small to be less intrusive. However, there is nothing that limits you to black and white cursors, and you can choose any two colors you like. The following example creates a large, x-shaped cursor that is red with black trim.

There are three ways that a pixel can be rendered in a cursor. It can be drawn in one of two colors, or it can be left transparent (not drawing a pixel lets the background pixel show through). This transparency option is the reason for the masking bitmap.