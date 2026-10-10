```
69 gtk_table_attach_defaults(GTK_TABLE(table),layout,  
70 0,1,0,1);  
71 gtk_table_attach(GTK_TABLE(table),vscroll,  
72 1,2,0,1,  
73 GTK_FILL,GTK_FILL,0,0);  
74 gtk_table_attach(GTK_TABLE(table),hscroll,  
75 0,1,1,2,  
76 GTK_FILL,GTK_FILL,0,0);  
77  
78 return(table);  
79 }  
80 void addButtons(GtkWidget *layout)  
81 {  
82 gint i;  
83 gint j;  
84 GtkWidget *button;  
85 gchar label[20];  
86  
87 for(i=100; i<1000; i += 100) {  
88 for(j=100; j<1000; j+= 50) {  
89 sprintf(label,"(%d,%d)",i,j);  
90 button = gtk_button_new_with_label(label);  
91 gtk_layout_put(GTK_LAYOUT(layout),button,i,j);  
92 }  
93 }  
94 }  
95 gint eventDelete(GtkWidget *widget,  
96 GdkEvent *event,gpointer data) {  
97 return(FALSE);  
98 }  
99 gint eventDestroy(GtkWidget *widget,  
100 GdkEvent *event,gpointer data) {  
101 gtk_main_quit();  
102 return(0);  
103 }
```

This example creates a 2x2 table that holds a layout widget in the upper-left corner, and holds scrollbars on the right and on the bottom— as shown in Figure 5-18. The layout has buttons placed at regular intervals across it. The label of each button is the values of its x and y coordinates within the layout container. So you are able to move the layout around and see all the buttons, the GtkAdjustment objects used by the layout are the same ones used by the scrollbar.

The makeLayout() function beginning on line 36 creates a table and inserts the various widgets into it. The table is a 2x2 grid with the layout in the upper left, a vertical scrollbar in the upper right, and a horizontal scrollbar in the lower left. There is nothing in the cell at the lower right.