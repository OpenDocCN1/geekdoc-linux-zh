```
93 
94 	button = gtk_button_new_with_label("Right");
95 	gtk_box_pack_end(GTK_BOX(box),button,TRUE,TRUE,5);
96 	gtk_widget_show(button);
97
98 	return(box);
99 }
100 gint eventDelete(GtkWidget *widget,
101 		GdkEvent *event,gpointer data) {
102 	return(FALSE);
103 }
104 gint eventDestroy(GtkWidget *widget,
105 		GdkEvent *event,gpointer data) {
106 	gtk_main_quit();
107 	return(0);
108 }
```

The call to makeBox() on line 28 creates the box and all its contents. The box is given to the container of the main window on line 29.

The makeBox() function beginning on line 36 creates a vertical box and inserts three widgets into it. On line 42, the box is created with the spacing between its contained widgets set to 30 pixels. The first widget is a button spaced and inserted into the box on lines 44 through 47. The second widget is a box returned from the call to makeMiddleBox() on line 49, and the third is a box returned from the call to makeBottomBox() on line 54. When displayed, the main window adjusts itself to fit the height and width of the box it contains. The height of the box, and thus the height of the window, is the sum of the height of each of these three widgets — plus two spaces of 30 pixels each.

The function makeMiddleBox() starting on line 61 creates a vertical box containing three buttons. This box is created with zero separation between the widgets, so its overall size is the width of the widest button and its height is the sum of all the button heights.

The function makeBottomBox() starting on line 84 creates a horizontal box that contains two buttons. The buttons are placed in the box as homogeneous (so they both are the same width) and instructed to expand (so they fill all the space available to them). Also, they both are given a 5-pixel spacing from its neighbor. The result is that, when the window is stretched horizontally, the buttons resize themselves and move to maintain the distances and ratios.

When you lay out a complicated window by packing boxes, you first need to figure out what your boxes are. It is not uncommon to have boxes nested three, four, or even five deep to get the exact layout you are after.