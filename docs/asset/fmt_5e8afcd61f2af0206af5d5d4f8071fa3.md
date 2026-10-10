
```c
/* example-start notebook notebook.c */

#include <gtk/gtk.h>

/* 此函数旋转标签页的位置 */
void rotate_button(GtkButton *button, GtkNotebook *notebook)
{
    gtk_notebook_set_tab_pos (notebook, (notebook)->tab_pos + 1)%4);
}

/* 添加/移除页标签和边框 */
void tabs_border(GtkButton *button, GtkNotebook *notebook)
{
    int tval = FALSE;
    int bval = FALSE;
    if (notebook)->show_tabs == 0)
        tval = TRUE;
    if (notebook)->show_border == 0)
        bval = TRUE;
    gtk_notebook_set_tabs(notebook, tval);
    gtk_notebook_set_show_border(notebook, bval);
}

/* 从笔记本中移除页面 */
void remove_page(GtkButton *button, GtkNotebook *notebook)
{
    guint page;

    page = gtk_notebook_get_current_page(notebook);
    gtk_notebook_remove_page(notebook, page);
    /* 需要刷新控件 --
    这强制控件重绘自己。 */
    gtk_widget_draw(GTK_WIDGET(notebook), NULL);
}

void delete (GtkWidget *widget, GtkWidget *event, gpointer data)
{
    gtk_main_quit();
}
```
