
```c
121        gtk_main();
122        exit(0);
123    }
124
125    void next(GtkWidget *widget, gpointer data )
126    {
127        int size = sizeof(cursor)/sizeof(struct cursorStruct);
128        if(++cursorIndex < size)
129            setCursor();
130        else
131            cursorIndex--;
132    }
133    void previous(GtkWidget *widget, gpointer data )
134    {
135        if(----cursorIndex >= 0)
136            setCursor();
137        else
138            cursorIndex++;
139    }
140    void setCursor()
141    {
142        if(cur != NULL)
143            gdk_cursor_destroy(cur);
144        cur = gdk_cursor_new(cursor[cursorIndex].type);
145        gdk_window_set_cursor(topLevel->window,cur);
146        gtk_label_set_text(GTK_LABEL(nameLabel),
147            cursor[cursorIndex].name);
148    }
149
150    GtkWidget *makeBox()
151    {
152        GtkWidget *buttonBox;
153        GtkWidget *box;
154        GtkWidget *button;
155
156        buttonBox = gtk_hbox_new(TRUE,10);
157
158        button = gtk_button_new_with_label("Previous");
159        gtk_box_pack_start(GTK_BOX(buttonBox),button,
160            FALSE,FALSE,0);
161        gtk_signal_connect(GTK_OBJECT(button),"clicked",
162            GTK_SIGNAL_FUNC(previous),NULL);
163
164        button = gtk_button_new_with_label("Next");
165        gtk_box_pack_start(GTK_BOX(buttonBox),button,
166            FALSE,FALSE,0);
167        gtk_signal_connect(GTK_OBJECT(button),"clicked",
168            GTK_SIGNAL_FUNC(next),NULL);
169
170        box = gtk_vbox_new(FALSE,0);
171
172    nameLabel = gtk_label_new("");
173
174    gtk_box_pack_start(GTK_BOX(box),nameLabel,
175        FALSE,FALSE,0);
176
177    gtk_box_pack_start(GTK_BOX(box),buttonBox,
178        FALSE,FALSE,0);
179
180    return(box);
181 }
182
183 gint eventDelete(GtkWidget *widget,
184     GdkEvent *event, gpointer data) {
185     return(FALSE);
186 }
187
188 gint eventDestroy(GtkWidget *widget,
189     GdkEvent *event, gpointer data) {
190     gtk_main_quit();
191     return(0);
192 }
```

This program displays the window shown in Figure 7-5. The window displays the name of a cursor and the cursor itself. It has two buttons that can be used to move back and forth through the list changing both the displayed name and cursor. The name displayed is the one that can be used to create a cursor by calling `gdk_cursor_new()`.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_214_0.png)

**Figure 7-5:** The name and appearance of one of the built-in cursors

Lines 16 through 97 define an array of structs holding the names and numeric values of the cursors. In the struct, the character string `name` is used to display the name for use in your call to `gdk_cursor_new()`, and the `type` is the enum value used to identify the cursor to the system.

Lines 117 through 119 create the window to be displayed, add it to the top-level window, then call `setCursor()` to set the cursor to the current one in the table. (The default index is 0.) Remember, the cursor cannot be modified for a window until after `gtk_widget_show()` is called.

The function makeBox() beginning on line 150 uses boxes to construct the layout. A horizontal box is used to hold the two buttons, and a vertical box is used to hold the label and the horizontal box. Each button is assigned a callback function—the “Previous” button calls previous() and the “Next” button calls next().

The callback function next() beginning on line 125 increments the cursor index value by one—if it is not already at the end of the array. The count of the number of members in the array is calculated by dividing the size of the entire array by the size of one member. The callback function previous() reduces the index by one if the index is larger than zero. In both functions, if the index value is incremented, a call is made to setCursor() to change the current cursor.

The setCursor() function beginning on line 140 changes the current cursor to the one in the array addressed by the index. If a cursor is already created, it is destroyed before a new one is created. If your program uses several cursors, you can create them once and reuse them as needed. A call is made to gdk_cursor_new() to create a GdkCursor object. Using this new cursor in a call to gtk_label_set_cursor() makes the new cursor become the one used by the top-level window and its descendants. (The cursor is also changed for the buttons and the label.) Finally, the text of the label is updated by a call to gtk_label_set_text() so the name of the cursor is displayed.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_215_0.png)

> **Note**
> The built-in cursors are all defined by the list of named values in the file gtk/gdk/gdkcursors.h, which is included by gtk/gdk/gtkcursors.h where it is used as the body of an enum. The list of cursors is quite stable—most of them have been a part of X for several years. However, it is possible that some new entries will be made and, if so, you will need to update the list of names and values compiled into this program.

# Create Cursor

It is a simple matter to create your own cursor. The bitmap utility can be used to create both the cursor and the mask to go with it. Then, these two bitmaps can be converted directly into the current cursor.

A cursor is normally black and white. It either has a black body with white trim surrounding it, or it has a white body with black trim. This way, the cursor can be placed on top of any color (including black or white) and still be visible. Also, cursors usually are kept small to be less intrusive. However, there is nothing that limits you to black and white cursors, and you can choose any two colors you like. The following example creates a large, x-shaped cursor that is red with black trim.

There are three ways that a pixel can be rendered in a cursor. It can be drawn in one of two colors, or it can be left transparent (not drawing a pixel lets the background pixel show through). This transparency option is the reason for the masking bitmap.

The two bitmaps are the same size. If the mask bit relating to the pixel is 0, then the pixel is not drawn—it is transparent. If the mask bit is 1, the pixel is drawn in one of two colors (depending on the value of the bit in the other bitmap).

The bitmap utility described earlier can be used to create a cursor. Both the cursor design and its mask are bitmaps. For this following example, the cursor design is the one shown in Figure 7-6 and its mask is shown in Figure 7-7. The cursor design is very much like the default root window cursor with the hot spot in its center.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_216_0.png)

**Figure 7-6:** The black and white pixels of a cursor

![](img/8bcc1ba72831c7d67cfc8b395deab95f_216_1.png)

**Figure 7-7:** The mask defining the outline of the cursor

The two bitmaps produced by the utility look like this:

```c
/* xbitmap.xbm */
#define xbitmap_width 24
#define xbitmap_height 24
#define xbitmap_x_hot 12
#define xbitmap_y_hot 11
static unsigned char xbitmap_bits[] = {
  0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x3c, 0x00,
  0x3c, 0x7c, 0x00, 0x3e, 0xfc, 0x00, 0x3f, 0xfc,
  0x81, 0x3f, 0xf8, 0xc3, 0x1f, 0xf0, 0xff, 0x0f,
  0xe0, 0xff, 0x07, 0xc0, 0xff, 0x03, 0x80, 0xff,
  0x01, 0x80, 0xff, 0x01, 0x80, 0xff, 0x01, 0x80,
  0xff, 0x01, 0xc0, 0xff, 0x03, 0xe0, 0xff, 0x07,
  0xf0, 0xff, 0x0f, 0xf8, 0xc3, 0x1f, 0xfc, 0x81,
  0x3f, 0xfc, 0x00, 0x3f, 0xc7, 0x3e, 0x3c,
  0x3f, 0x3c, 0x00, 0x00, 0x00, 0x00, 0x00};
```

```c
/* xmask.xbm */
#define xmask_width 24
#define xmask_height 24
static unsigned char xmask_bits[] = {
    0x00, 0x00, 0x00, 0x3c, 0x00, 0x7c, 0x7e, 0x00,
    0x7e, 0xfe, 0xc0, 0x07, 0xfe, 0x81, 0xff, 0xfe,
    0xc3, 0xff, 0xfc, 0xe7, 0x3f, 0xf8, 0xff, 0x1f,
    0xf0, 0xff, 0x0f, 0xe0, 0xff, 0x07, 0xc0, 0xff,
    0x03, 0x80, 0xff, 0x01, 0x80, 0xff, 0x01, 0xc0,
    0xff, 0x03, 0xe0, 0xff, 0x07, 0x0f, 0x0f,
    0xf8, 0xff, 0x1f, 0xfc, 0xe7, 0x3f, 0xfe, 0xc3,
    0x7f, 0xfe, 0x81, 0x7f, 0xfe, 0x00, 0x7f, 0x7e,
    0x00, 0x7e, 0x3e, 0x00, 0x7c, 0x00, 0x00, 0x00};
```

The following example program uses these bitmaps to create a cursor and assign it as the cursor to appear any time the mouse is over the top-level window of the application:

```c
1 /** xbmcursor.c **/
2 #include <gnome.h>
3
4 gint eventDelete(GtkWidget *widget,
5     GdkEvent *event, gpointer data);
6 gint eventDestroy(GtkWidget *widget,
7     GdkEvent *event, gpointer data);
8
9 #include "xbitmap.xbm"
10 #include "xmask.xbm"
11
12 static GdkColor oneColor = {0,0xFFFF,0x0000,0x0000};
13 static GdkColor zeroColor = {0,0x0000,0x0000,0x0000};
14
15 int main(int argc, char *argv[])
16 {
17     GtkWidget *topLevel;
18     GdkCursor *cursor;
19     GdkBitmap *bitmap;
20     GdkBitmap *mask;
21
22     gnome_init("lib/xbmcursor","1.0",argc,argv);
23     topLevel = gtk_window_new(GTK_WINDOW_TOPLEVEL);
24     gtk_window_set_default_size(GTK_WINDOW(topLevel),
25             150,150);
26
27     gtk_signal_connect(GTK_OBJECT(topLevel),"delete_event",
```
