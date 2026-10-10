```
129 {
    switch(style) {
130     case GDK_CAP_NOT_LAST: return("not last");
132     case GDK_CAP_BUTT: return("butt");
133     case GDK_CAP_ROUND: return("round");
134     case GDK_CAP_PROJECTING: return("projecting");
135     default: return("");
136     }
137 }
138 static char *joinStyleString(gint style)
139 {
    switch(style) {
140     case GDK_JOIN_MITER: return("miter");
142     case GDK_JOIN_ROUND: return("round");
143     case GDK_JOIN_BEVEL: return("bevel");
144     default: return("");
145     }
146 }

147 
148 gint eventDelete(GtkWidget *widget,
149     GdkEvent *event,gpointer data) {
150     return(FALSE);
151 }
152 gint eventDestroy(GtkWidget *widget,
153     GdkEvent *event,gpointer data) {
154     gtk_main_quit();
155     return(0);
156 }
```

Lines 31 through 35 create a drawing area, insert it into the main window, and connect the callback function `listValues()`, which is triggered by the "realize" signal, meaning the callback is called just once—when the window is fully constructed and capable of being displayed. It is necessary to wait until the window is realized because there are GdGC values available only then.

The callback function `listValues()`, beginning on line 41, prints every value from a graphics context found in the widget. There are a number of graphics contexts in the widget, which I describe later in this chapter, but this program gets the one named `white_gc` on line 47. The values in a GdGC object are not accessible directly, so, on line 48, the call to `gdk_gc_get_values()` fills a GdGCValues struct with information in the GdGC. The rest of this function prints the values.

Lines 50 through 55 display information about the colors. There are two colors stored in a graphics context: one for the foreground and one for the background. All painting and drawing is done using the foreground color, while clearing and erasing is performed using the background color.

Line 56 lists information about the font. About all that is known about it is an internal ID number, the maximum number of pixels a character may ascend above the base line, and the maximum number of pixels a character may descend below the base line. Adding these two figures together gives you the height of the tallest