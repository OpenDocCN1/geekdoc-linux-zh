```
91            sprintf(string,
92                "This is the text of the %s text page.. ",str);
93            for(i=0; i<80; i++) {
94                gtk_text_insert(GTK_TEXT(text),NULL,NULL,NULL,
95                    string,-1);
96            }
97        }
98        return(text);
99    }
100 gint eventDelete(GtkWidget *widget,
101                GdkEvent *event,gpointer data) {
102        return(FALSE);
103    }
104 gint eventDestroy(GtkWidget *widget,
105                GdkEvent *event,gpointer data) {
106        gtk_main_quit();
107        return(0);
108    }
```

![](bbox=[0.17, 0.44, 0.38, 0.58])

# **Figure 5-22:** A notebook containing five pages

The function `makeNotebook()`, starting on line 37, creates the notebook and stores several pages into it. The notebook is created and configured on lines 42 through 44. The pages are created and inserted into the notebook container on lines 46 through 69. (The actual pages are created by the `makeButtonPage()` and `makeTextPage()` functions starting on lines 73 and 84.)

The notebook container can position the row of tabs against any one of its four sides. The call to `gtk_notebook_set_tab_pos()` is used to set the position of the tabs. The value `GTK_POS_TOP` places the buttons on top (as shown in Figure 5-22). Using the value `GTK_POS_BOTTOM` places the tabs on bottom as they are in Figure 5-23. Using `GTK_POS_LEFT` places the tabs on the left, producing a window like the one shown in Figure 5-24. The value `GTK_POS_RIGHT` places the tabs on the right. The default, and probably the most used position, is `GTK_POS_TOP`.