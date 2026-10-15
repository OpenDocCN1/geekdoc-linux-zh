
`gtk_radio_button_new_with_group`的第一个参数是同组中现有单选按钮的指针。如果你传递`NULL`，则创建一个组。第二个参数是一个布尔值，指示新按钮是否默认选中。

和切换按钮一样，单选按钮发射`"toggled"`信号。你可以利用它来响应用户的选择。

## 第 5 章（续）

从那里开始，你可以继续添加并显示。最后一步是获取更新的列表指针。我们在第 2 章中讨论过这个。每当你向列表添加项时，你都需要跟踪列表的变化，因为 GLib 可能会更改头部指针。然而，对于所有的 GLib 列表函数，它们都会向你返回更新的列表指针。然而，到目前为止我们唯一返回值是单选按钮的指针。要获取更新的列表指针，你需要让单选按钮将其给你。这是通过`gtk_radio_button_group`实现的。该函数如下：

```
GList * gtk_radio_button_group ( GtkRadioButton * radio_button );
```

只需传入你的单选按钮指针，你就能得到列表头的指针。

如你所示，与我们看过的其他小部件相比，有许多步骤需要确保一切协调工作。如果出错，通常情况下应用程序将会停止并发生段错误（segmentation fault），这是意料之外的。因此，许多人会编写一个函数来构建单选按钮，并在单个函数调用中处理所有步骤。想要自己尝试，只需输入、编译并运行`radiobutton.c`：

```c
/**
 * radiobutton.c
 * 展示单选按钮及其组在实际运行效果的示例
 */

#include <gtk/gtk.h>
```

```c
void CloseApp ( GtkWidget * window, gpointer data )
{
  gtk_main_quit ( );
}
```

```c
/* 向指定的窗口添加一组单选按钮 */

GSList * AddRadioButton (GtkWidget *box, gchar *label, GSList *group)
{
  GtkWidget * radio;

  /* 创建一个单选按钮，并将其标签添加到列表中 */
  radio = gtk_radio_button_new_label ( group, label );

  /* 将单选按钮放入布局框中 */
  gtk_box_pack_start ( GTK_BOX ( box ), radio, TRUE, 5 );

  /* 返回新的列表指针 */
  return ( gtk_radio_button_group ( GTK_RADIO_BUTTON ( radio ) ) );
}
```

```c
gint main ( int argc, gchar * argv[] )
{
  GtkWidget * window;
  GtkWidget * box;
  GSList * group = NULL;
```

```c
  gtk_init ( &argc, &argv );

  window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
  gtk_window_set_title ( GTK_WINDOW ( window ), "Radio Buttons" );
  gtk_window_default_size ( GTK_WINDOW ( window ), 320, 200 );
  gtk_container_set_border_width ( GTK_CONTAINER ( window ), 10 );
  gtk_signal_connect ( GTK_OBJECT ( window ), "destroy",
                       GTK_SIGNAL_FUNC ( CloseApp ),
                       NULL );

  box = gtk_vbox_new ( TRUE, 5 );
```

- 使用我们的`AddRadioButton`函数来构建单选按钮。
- 传入你想要将新单选按钮添加的框
- 按钮的标题以及指向
- 单向链表的指针

```c
  group = AddRadioButton ( box, "First option", group );
  group = AddRadioButton ( box, "Second option", group );
  group = AddRadioButton ( box, "Third option", group );
  group = AddRadioButton ( box, "Final option", group );
```

```c
  gtk_container_add ( GTK_CONTAINER ( window ), box );
  gtk_widget_show_all ( window );
  gtk_main ();
  return 0;
}
```

# 第 5 章

运行它，你将得到：

![](img/aa3546013f120531cd191b770d85869c_155_0.png)

此应用程序大部分工作位于代码顶部的`AddRadioButton`函数中。这代表了创建单选按钮并从中获取更新指针所需要经历的步骤蓝图（不包括连接信号处理程序）。

除此之外，单选按钮的工作方式与我们已经看过的复选按钮和切换按钮相同。单选按钮是复选按钮的直接后代，而你已经知道，复选按钮是切换按钮的后代。

## 框架 (Frames)

到目前为止，我们涵盖了 GTK+ 中的基础组件，你应该已经开始创建相当整洁的用户界面了。然而，缺少了一些东西。有时根据功能可见地对窗口中的组分组非常方便。例如，你可能希望窗口的一部分显示员工姓名列表，而另一部分显示特定员工的详情。

框架对于管理这种拆分很有用，它可以在组件组周围绘制一个精美的边框。事实上，框架无非是一个可见的容器，就像窗口一样。你创建它，将其添加到窗口或你的布局窗口中，然后将其他布局组件封装其中。就像窗口一样，`GtkFrame`只能包含一个组件，因此在开始向其添加组件之前，记住向它添加一个布局框或表格是非常重要的。

创建一个非常简单，只需调用`gtk_frame_new`：

```c
GtkWidget * gtk_frame_new ( const gchar * label );
```

# 组件奇技 (Widget Wonders)

它接收一个显示在框架顶部框上的文本字符串指针。或者，你可以传递`NULL`以便框架上没有标题。通常，它对齐到顶部框的左侧，你可以通过调用以下函数来更改：

```c
void gtk_frame_set_label_align ( GtkFrame * frame , gfloat xalign
                                , gfloat yalign );
```

`xalign`和`yalign`参数在 0.0 到 1.0 之间，并指定跨越框架边界的比例来显示标题。例如，`xalign`值为 0 将标题左对齐，而 0.5 的值将其置于中间。

你还可以更改框架边框的外观和感受。这被称为阴影类型：

```c
void gtk_frame_set_shadow_type ( GtkFrame * frame, GtkShadowType type );
```

`Type`可以是`GTK_SHADOW_NONE`、`GTK_SHADOW_IN`、`GTK_SHADOW_OUT`、`GTK_SHADOW_ETCHED_IN`或`GTK_SHADOW_ETCHED_OUT`中的。默认情况下，阴影类型为`GTK_SHADOW_ETCHED_IN`。

查看`framesample.c`以查看效果：

```c
/**
 * framesample.c
 * 创建框架的小程序
 */

#include <gtk/gtk.h>

void CloseApp ( GtkWidget * window, gpointer data )
{
  gtk_main_quit ( );
}

int main ( int argc, char * argv[] )
{
  GtkWidget * window;
  GtkWidget * box;
  GSList * group = NULL;

  gtk_init ( &argc, &argv );

  window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
  gtk_window_set_title ( GTK_WINDOW ( window ), "Radio Buttons" );
  gtk_window_default_size ( GTK_WINDOW ( window ), 320, 200 );
  gtk_container_set_border_width ( GTK_CONTAINER ( window ), 10 );
  gtk_signal_connect ( GTK_OBJECT ( window ), "destroy",
                       GTK_SIGNAL_FUNC ( CloseApp ),
                       NULL );

  box = gtk_vbox_new ( TRUE, 5 );

  /* 使用我们的 AddRadioButton 函数来构建单选按钮。
   * 传入你想要将新单选按钮添加的框
   * 以及按钮的标题以及指向
   * 单向链表的指针 */
  group = AddRadioButton ( box, "First option", group );
  group = AddRadioButton ( box, "Second option", group );
  group = AddRadioButton ( box, "Third option", group );
  group = AddRadioButton ( box, "Final option", group );

  gtk_container_add ( GTK_CONTAINER ( window ), box );
  gtk_widget_show_all ( window );
  gtk_main ();
  return 0;
}
```

# 第 6 章

GTK+ 实际上包含了两个列表小部件。它们是高级且高度可配置的`GtkList`小部件，以及传统的、更简单的`GtkList`小部件。我们将关注后者。虽然`GtkList`提供了更多功能（你将在本章末尾看到），但对于那些不需要`GtkList`高级特性的人来说，`GtkList`仍然是一个非常有用的列表小部件。

如果你和我一样，那么当你提到列表框（listbox）时，会认为它是一个包含项目、并在用户移动其中项目时进行滚动的“箱子”。对吧？嗯，它们在 GTK+ 中的工作方式并非完全如此。

`GtkList`实际上是一个容器。你创建小部件并将它们添加到列表中，通常你创建的小部件是`GtkItems`。这些`GtkListItem`也是容器，因此你可以在带标签或不带标签的情况下创建它们（就像创建按钮时一样）。如果你创建一个不带标签的`GtkListItem`，那么你可以自由地将其添加到你喜欢的任何类型的小部件中，从按钮到像素图图形（关于这些，将在第 10 章中详细介绍）。

> 我第一次遇到`GLists`并看到它们的工作原理时，被其不寻常之处震惊了。我习惯了简单地向列表框添加字符串并让它们神奇地出现。去创建小部件并将它们添加到箱子里似乎是多此一举。然而，`GtkList`小部件非常出色，与其他操作系统的控件不同，GTK+ 不限制你只能列表一种特定类型的数据。如果你想有一个图像列表，可以像创建文本列表一样容易。

## 那么，它是如何工作的？

创建一个列表框与创建任何其他类型的小部件一样。需要调用以下函数：

```
GtkWidget * gtk_list_new ();
```

返回值始终是指新创建的小部件的指针。要向列表框中添加项目，你有几种选择。由于`GtkList`是一个容器，你可以简单地创建一个`GtkListItem`小部件，显示它，并通过调用`gtk_container_add`将其添加到容器中。或者，你可以创建一些`GtkListItem`小部件，将它们添加到一个`GList`中（记住第 2 章），然后将该`GList`添加到`GtkList`小部件中。让我们通过一个小示例程序来看向第一个列表添加单个项目。

```c
/*
 * listsample.c
 * 一个显示如何向列表框添加单个项目的小型程序
 */
```

```c
#include <gtk/gtk.h>

GtkWidget * listbox;

void CloseTheApp ( GtkWidget * window, gpointer data )
{
  gtk_main_quit ( );
}
```

```c
/* 向列表框添加一个字符串 */
void AddStringToList ( gchar * text_string )
{
  GtkWidget * listitem;

  listitem = gtk_list_item_new_with_label ( text_string );
  gtk_container_add ( GTK_CONTAINER(listbox), listitem);
  gtk_widget_show ( listitem);
}
```

```c
/* 按钮“点击”处理器 */
void AddButtonClicked ( GtkButton * button, gpointer entrybox )
{
  AddStringToList ( gtk_entry_get_text ( GTK_ENTRY ( entrybox ) ) );

  /* 清空输入框 */
  gtk_entry_set_text ( GTK_ENTRY ( entrybox ), "" );
}
```

```c
/* 输入 HBox 构造器 */
GtkWidget * BuildEntryHBox ( GtkWidget * responseButton ) {
  GtkWidget * hBox;
  GtkWidget * label;
  GtkWidget * entry;

  hBox = gtk_hbox_new ( TRUE, 5 );
```

```c
  label = gtk_label_new ("Enter the string to add :");
  gtk_box_pack_start ( GTK_BOX(hBox ), label, TRUE, TRUE, 2 );
  gtk_widget_show ( label );
```

```c
  entry = gtk_entry_new ();
  gtk_box_pack_end ( GTK_BOX(hBox ), entry, TRUE, TRUE, 2 );
  gtk_widget_show ( entry );
```

```c
  /* 将我们的输入框连接到按钮的点击信号处理器 */
  gtk_signal_connect ( GTK_OBJECT ( responseButton ),
                       "clicked",
                       GTK_SIGNAL_FUNC(AddButtonClicked),
                       entry );
```

```c
  gtk_widget_show ( hBox );
```

```c
  return hBox;
}
```

```c
/* 主 VBox 构造器 */
GtkWidget * MainVBox ( ) {
  GtkWidget * mainBox;
  GtkWidget * button;
```

```c
  mainBox = gtk_vbox_new ( FALSE, 5 );
```

```c
  button = gtk_button_new_with_label ("Add String");
```

```c
  gtk_box_pack_start ( GTK_BOX(mainBox ), BuildEntryHBox ( button ),
                       FALSE, FALSE, 2 );
```

```c
  gtk_box_pack_start ( GTK_BOX(mainBox ), button, FALSE, FALSE, 2 );
```

```c
  listbox = gtk_list_new ();
  gtk_box_pack_end ( GTK_BOX(mainBox ), listbox, TRUE, TRUE, 2 );
  gtk_widget_show ( listbox );
```

```c
  gtk_widget_show ( mainBox ); // 注意：此处原文应为mainBox
  return mainBox; // 注意：此处原文应为mainBox
}
```

```c
/* 主函数 */
int main (int argc, char *argv[])
{
  GtkWidget * window;

  gtk_init ( &argc, &argv );

  window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
  gtk_window_set_title ( GTK_WINDOW(window), "List Demo" );
  gtk_window_set_default_size ( GTK_WINDOW(window), 200, 200 );
  gtk_signal_connect ( GTK_OBJECT(window), "destroy", GTK_SIGNAL_FUNC(CloseTheApp), NULL );

  gtk_container_add ( GTK_CONTAINER(window), MainVBox() );
  gtk_widget_show ( window );

  gtk_main();

  return 0;
}
```

## 列表与批量数据小部件
