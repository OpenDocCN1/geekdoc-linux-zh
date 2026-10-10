```
```
49      }
50      GtkWidget *makeTable() {
51          int r;
52          int c;
53          int index;
54          GtkWidget *table;
55          GtkWidget *button;
56
57          table = gtk_table_new(2,4,HOMOGENEOUS);
58          gtk_widget_show(table);
59
60          for(r=0; r<2; r++) {
61              for(c=0; c<4; c++) {
62                  index = (r * 4) + c;
63                  button = gtk_button_new_with_label(
64                          op[index].text);
65                  gtk_table_attach(GTK_TABLE(table),button,
66                          c,c+1,r,r+1,
67                          op[index].setting,
68                          op[index].setting,
69                          X_MARGIN,
70                          Y_MARGIN);
71                  gtk_widget_show(button);
72              }
73          }
74          return(table);
75      }
76      gint eventDelete(GtkWidget *widget,
77                  GdkEvent *event,gpointer data) {
78          return(FALSE);
79      }
80      gint eventDestroy(GtkWidget *widget,
81                  GdkEvent *event,gpointer data) {
82          gtk_main_quit();
83          return(0);
84```

```

Lines 10 through 11 define whether the table is homogeneous and how much padding to add around the widgets. The struct array defined on lines 14 through 25 contains all the possible combinations for the options, along with a text label for each one. Line 57 creates a 2x4 table to hold all the widgets, and the loop beginning on lines 60 and 61 creates and inserts buttons into all the cells. Figure 4-19 shows the window as it first appears when the program is run. Figure 4-20 shows the window after using the mouse to expand it.

![](bbox=[0.18, 0.83, 0.33, 0.93])

Figure 4-19: A nonhomogeneous window at its minimum size