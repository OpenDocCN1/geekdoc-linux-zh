
`member_search_list = g_slist_append(member_search_list, GINT_TO_POINTER(id));`

```c
appbar_text = g_strdup_printf("Found result searching for \n%%s", entry1_text);

gnome_appbar_set_status(GNOME_APPBAR(lookup_widget(
    GTK_WIDGET(button), "search_appbar")), appbar_text);
```

```c
else
{
    dvd_gui_show_result("member_search",
    dvd_member_search(entry1_text, &ids, &count));
    appbar_text = g_str_printf("Found %d result(s) searching for\n%%s*", count, entry1_text);
    gnome_appbar_set_status(GNOME_APPBAR (
    lookup_widget(GTK_WIDGET (button), "search_appbar")),
    appbar_text);
    while (count--)
    member_search_slist = g_list_append(member_search_slist,
    GINT_TO_POINTER(ids[i++]));
    update_member_search_clist();
}
```

搜索磁盘将列出与标题相关的磁盘，如果已借出，则显示借出成员的编号：

```c
if (current_page == DISK_PAGE)
{
    entry1 = lookup_widget(GTK_WIDGET(button), "disk_spin_button");
    disk = gtk_spin_button_get_value(GTK_SPIN_BUTTON(entry1));
    clist = GTK_LIST(lookup_widget(GTK_WIDGET(button),
    "disk_search_clist"));
    dvd_gui_show_result("disk_search",
    dvd_disk_search(disk, &ids, &count));
    g_slist_free(disk_search_list);
    disk_search_list = NULL;
    appbar_text = g_strdup_printf("Found %d Disk(s) for Title ID %d", count, diskid);
    gnome_appbar_set_status(GNOME_APPBAR(
    lookup_widget(GTK_WIDGET(button), "search_appbar")), appbar_text);
    while (count--)
    disk_search_list = g_list_append(disk_search_list,
    GINT_TO_POINTER(ids[i++]));
    update_disk_search_clist();
}
```

### on_search_close

```c
void
on_search_close_clicked (GtkButton *button,
gpointer)
{
    gtk_widget_hide(search_window);
}
```

### on_search_clear

此函数清除当前打开页面的 `clist`：

```c
void
on_search_clear_clicked (GtkButton *button,
gpointer)
{
    gint current_page;
    GtkWidget *search_notebook;
    GtkWidget *clist;
    search_notebook = lookup_widget(GTK_WIDGET(button), "search_notebook");
    current_page = gtk_notebook_get_current_page(GTK_NOTEBOOK(search_notebook));
    switch (current_page) {
        case TITLE_PAGE:
            clist = lookup_widget(GTK_WIDGET(button), "title_search_clist");
            break;
        case MEMBER_PAGE:
            clist = lookup_widget(GTK_WIDGET(button), "member_search_clist");
            break;
        case DISK_PAGE:
            clist = lookup_widget(GTK_WIDGET(button), "disk_search_clist");
            break;
        default:
            g_assert_not_reached();
    }
    gtk_clist_clear(GTK_CLIST(clist));
    gnome_appbar_set_status(GNOME_APPBAR(lookup_widget(GTK_WIDGET(button), "search_appbar")), "Cleared");
}
```

### on_dvd_search_clist_button_press_event

当在标题列表或成员列表内处点击鼠标右键时，此函数会显示相关的弹出菜单：

```c
boolean
on_dvd_search_clist_button_press_event (GtkWidget *widget,
GdkEventButton *event)
{
    GtkWidget *menu;
    GtkList *clist;
    int row, column;
    g_return_val_if_fail(widget != NULL, FALSE);
    menu = create_dvd_popup_menu();
    if (event->type == GDK_BUTTON_PRESS) {
      GtkButton *buttonevent = (GtkButton *) event;
      if (buttonevent->button == GDK_BUTTON1_MASK) {
        clist = GTK_LIST(gtk_list_get_selection_info(clist)); // 注意：原文此处逻辑错误
        // 根据标准 GTK+ 列表重新评估：
        if (gtk_list_get(clist, buttonevent->x, buttonevent->y, &row, &column)) {
            // ... 
        }
      }
    }
}
```

剩余函数是弹出菜单四个菜单项的回调函数：租借、预约、编辑和删除。

### on_search_menu_rent_activate

此函数判断打开的是标题页还是成员页，并调用 `do_rent_dvd_dialog` 将所选行的标题或成员 ID 作为参数传递：

```c
void
on_search_menu_rent_activate (GtkMenuItem *menuitem,
gpointer user_data)
{
    int current_page;
    int id;
    dvd_store_member_member member;
    current_page = gtk_notebook_get_current_page (GTK_NOTEBOOK
  (lookup_widget(search_window, "search_notebook")));
    if (current_page == TITLE_PAGE) {
        g_return_if_fail (title_search_slist != NULL);
```
