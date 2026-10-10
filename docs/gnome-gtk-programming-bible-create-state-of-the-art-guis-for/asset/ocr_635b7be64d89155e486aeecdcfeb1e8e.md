```
```
172
nameLabel = gtk_label_new("");
173
gtk_box_pack_start(GTK_BOX(box),nameLabel,
174	FALSE,FALSE,0);
175
gtk_box_pack_start(GTK_BOX(box),buttonBox,
176	FALSE,FALSE,0);
177
return(box);
179 }
180
gint eventDelete(GtkWidget *widget,
182	GdkEvent *event,gpointer data) {
183	return(FALSE);
184 }
185
gint eventDestroy(GtkWidget *widget,
186	GdkEvent *event,gpointer data) {
187	gtk_main_quit();
188	return(0);
189 }
```
```

This program displays the window shown in Figure 7-5. The window displays the name of a cursor and the cursor itself. It has two buttons that can be used to move back and forth through the list changing both the displayed name and cursor. The name displayed is the one that can be used to create a cursor by calling `gdk_cursor_new()`.

![](bbox=[0.12, 0.54, 0.43, 0.7])

**Figure 7-5:** The name and appearance of one of the built-in cursors

Lines 16 through 97 define an array of structs holding the names and numeric values of the cursors. In the struct, the character string `name` is used to display the name for use in your call to `gdk_cursor_new()`, and the `type` is the enum value used to identify the cursor to the system.

Lines 117 through 119 create the window to be displayed, add it to the top-level window, then call `setCursor()` to set the cursor to the current one in the table. (The default index is 0.) Remember, the cursor cannot be modified for a window until after `gtk_widget_show()` is called.