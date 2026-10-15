
```c
/** 无处不在的 main () 函数 */
gint main (int argc, gchar * argv[])
{
    gnome_init ( app_name, app_version, argc, argv );

    BuildMainWindow ( app_name, app_version );

    gtk_ main ();
    return 0;
}
```

由于应用程序代码是以非常内聚的方式编写，`main` 函数可能比你预期的要小得多。毕竟，它只专注于一件事——启动应用程序。

在初始化 GNOME 后，通过调用 `gnome_init`，调用了 `BuildMainWindow` 函数——其唯一目的是构建主窗口。该代码位于 `mainwindow.c` 中，我们稍后会查看。

## 应用程序：图像查看器

不过，关于 `main` 函数值得注意的是，发现和修复 Bug 是多么容易。这听起来可能是一句显而易见的话，但用户界面很容易发现的。

即使那是最纯粹的操作方式，按钮处理程序的点击也可以与菜单项点击处理程序正常工作。在底层，这两个处理句程序的格式完全相同；它们都接受指针作为参数。第一个指向发射信号的小部件的指针，第二个是程序员定义的指向某些通用数据的指针。

## 用户界面

现在让我们来看看应用程序的用户界面是如何构建的。再次，这部分代码存在于 `main.c` 源文件中。

```c
void BuildMainWindow( gchar * appname, gchar * appversion ) {
    /* 创建 GnomeApp 部件并将其置于屏幕顶部 */
    gnome_app_new( appname, "Image Viewer" );

    gtk_window_set_default_size( GTK_WINDOW ( window ),
        gtk_screen_width( ) - 100, 80 );

    gtk_widget_set_position( window, 0, 0 );

    /* 然后，连接主窗口的信号处理程序 */
    gtk_signal_connect( GTK_OBJECT ( window ),
        "delete_event", GTK_SIGNAL_FUNC ( QueryShutdown, NULL ) );

    gtk_signal_connect( GTK_OBJECT ( window ),
        "destroy", GTK_SIGNAL_FUNC ( CloseApp, NULL ) );

    /* 构建菜单栏 */
    gnome_app_create_menu( GNOME_APP ( window ), menu_bar );

    /* 构建工具栏 */
    gnome_app_create_toolbar( GNOME_APP ( window ), toolbar_icons );

    /* 最后，显示窗口 */
    gtk_widget_show( window );

    /* 清除活动窗口指针，因为程序刚刚启动 * */
    ClearActiveWindow( );
}
```

`BuildMainWindow` 是一个非常直观的函数，在目前没有任何让你感到惊讶的内容。它是应用程序包含界面的主窗口。该函数立刻让你印象深刻的一点是它非常小。原因当然是 GNOME 根据在源文件头部定义的 `GnomeUIInfo` 结构体自动构建了用户界面的大部分。我们稍后会来看这一点。

我们做的第一件事是设置 `GnomeApp` 部件的大小和位置。目标是让主窗口位于屏幕顶部并横跨屏幕的大部分区域。这很容易做到。使用 `gtk_widget_set_position` 函数将窗口的默认位置设置为 `0, 0` —— 它是屏幕左上角的坐标。宽度通过调用 `gdk_screen_width` 确定，该函数返回一个表示屏幕像素宽的整数。由于许多窗口系统用户倾向于在屏幕一侧运行某种应用程序栏，代码从屏幕宽度中减去 100 像素，以确定一个能够容纳用户可能拥有的任何栏的窗口宽度。

## 第 18 章

![](img/aa3546013f120531cd191b770d85869c_487_0.png)

如果你喜欢，可以随意从代码中删除尺寸函数的调用。到那时，窗口的大小将仅为容纳菜单和工具栏所需的尺寸。这实际上只是个人偏好的问题。接下来连接了窗口的 `delete_event` 和 `destroy` 信号的信号处理程序——我们在上一节中看过它们了，所以我不再重复赘述。

最后，将菜单和工具栏添加到窗口中。由于这些是使用 `GnomeUIInfo` 结构体构建的，因此不需要其他工作即可将这些元素连接并与其信号处理程序协同工作。关于信号处理程序的信息，以及工具栏按钮和菜单项的外观效果，都定义在 `GnomeUIInfo` 结构体中。

```c
/*====================/
static GnomeUIInfo file_menu[] = {
    GNOMEUIINFO_MENU_OPEN_ITEM (FileOpenHandler, NULL),
    GNOMEUIINFO_MENU_CLOSE_ITEM (FileCloseHandler, NULL),
    GNOMEUIINFO_SEPARATOR,
    GNOMEUIINFO_MENU_EXIT_ITEM (FileExitHandler, NULL),
    GNOMEUIINFO_END
};
static GnomeUIInfo help_menu[] = {
    GNOMEUIINFO_MENU_ABOUT_ITEM (HelpAboutHandler, NULL),
    GNOMEUIINFO_END
};
static GnomeUIInfo menu_bar[] = {
    GNOMEUIINFO_SUBTREE ("_File", file_menu),
    GNOMEUIINFO_SUBTREE ("_Help", help_menu),
    GNOMEUIINFO_END
};

/*==================== TOOLBARS =================*/
static GnomeUIInfo toolbar_icons[] = {
    {GNOME_APP_UI_ITEM, "Open", "Load a graphic", FileOpenHandler, NULL, NULL,
     GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_OPEN},
    {GNOME_APP_UI_ITEM, "Close", "Close the current graphic",
     FileCloseHandler, NULL, NULL,
     GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_CLOSE},
     GNOMEUIINFO_SEPARATOR,
    {GNOME_APP_UI_ITEM, "Rotate", "Rotate image", RotateHandler, NULL, NULL, NULL,
     GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_REDO},
    {GNOME_APP_UI_ITEM, "Rotate", "Rotate image", RotateHandler, NULL, NULL,
     GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_REDO},
...
```

*(注：原始文本中存在大量 OCR 识别错误和重复乱码，已根据高级文档工程师逻辑对内容进行了清理和翻译处理。)*

要显示图像，你将文件名传递给 `ShowImage` 函数，该函数位于 `ImageWindow.c` 中，代码如下：

```c
void ShowImage ( gchar * filename ) {
  GdkImlibImage * image;
  GtkWidget * window;
  GtkWidget * messagebox;

  /* Attempt to load up the specified image */
  image = gdk_imlib_load_image ( filename);

  /* If the resulting image is NULL, then the load failed...
     tell the user */
  if ( image == NULL) {
    messagebox = gnome_message_box_new ("Sorry, I was unable to work with the specified file",
      GTOME_MESSAGE_BOX_ERROR, GTOME_STOCK_BUTTON_OK, NULL);
    gnome_dialog_run_and_close ( GNOME_DIALOG ( messagebox ) );
    return;
  }

  /* Create a window in the usual way, with the filename as the title */
  window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
  gtk_window_set_title ( GTK_WINDOW ( window ), filename );

  /* Set the newly loaded image into the window */
  SetImage( window, image );

  /* Connect up the window's signal handlers */
  gtk_signal_connect ( GTK_OBJECT ( window ),
    "destroy", GTK_SIGNAL_FUNC ( DestroyWindow ), image );

  gtk_signal_connect ( GTK_OBJECT ( window ),
    "focus_in_event", GTK_SIGNAL_FUNC ( Focus ), image );

  /* Finally, show the window */
  gtk_widget_show ( window );
}
```

应用程序中通过结合 `GdkImlibImage` 对象和 `GnomePixmap` 控件来显示图像。`GnomePixmap` 控件能够加载并显示几乎任何你可能需要的图形格式。然而，正如我在本节早些提到的，GNOME 中没有用于操作该图像的函数（例如旋转和翻转图像的函数）。因此，我们使用 `GdkImlibImage` 对象来加载和处理用户选择的图形文件，然后再将该图像用于设置 `GnomePixmap` 图像。

## 第 18 章

`ShowImage` 中的前几行代码只是尝试加载传递给函数的文件。如果加载失败（因为文件名无效，或者指定了 `GdkImlibImage` 无法处理的文件格式），则会向用户显示消息框，告诉他们出现了问题。然后函数退出。

![](img/aa3546013f120531cd191b770d85869c_491_0.png)

假设图像加载按计划进行，接下来的代码行将创建窗口，并将文件名设置为窗口标题。`ImageViewer` 并没有费心为窗口设置默认大小，因为 `GnomePixmap` 控件会自动调整为图像的大小，并随之改变窗口大小。

接下来通过调用 `SetImageIntoWindow` 创建 `GnomePixmap` 并将其设置窗口中。最后，设置窗口接收焦点和被销毁的信号处理器，并显示窗口。我们稍后会查看这些特殊处理器，但首先，让我们来看 `SetImageIntoWindow`。

```c
void SetImageIntoWindow ( GtkWidget * window, GdkImlibImage * image ) {
  GtkWidget * pixmap;

  /* Check to see if there is already a child in the window */
  if ( GTK_BIN ( window )->child != NULL ) {
    /* Destroy the child if there is one */
    gtk_widget_destroy ( GTK_BIN ( window )->child );

    /* Create a new Gnome from the passed in image */
    pixmap = gnome_pixmap_new_from_imlib ( image );

    /* Add the GnomePixmap into the window and show it */
    gtk_container_add ( GTK_CONTAINER ( window ), pixmap );
    gtk_widget_show ( pixmap );
  }
```

该函数在初始图像加载以及图像变化（翻转或旋转时）时都会被调用。因此，它必须是一个智能函数，在调用之前清理窗口中已嵌入的任何内容。

第一行代码执行了此操作。`GtkWindow` 派自 `GtkBin`，这是一个只能包含单个子元素的特殊容器。它做的第一件事是检查窗口当前是否连接了任何子控件。可能只有一个，即显示加载图像的 `GnomePixmap`。因此，如果子控件指针不为空，则销毁窗口中现有的 `GnomePixmap` 控件。

处理完后，代码开始创建显示加载图像的 `GnomePixmap` 控件。这是通过调用 `gnome_pixmap_new_from_imlib` 实现的，传入相关的 `GdkImlibImage`。

新创建的 `GnomePixmap` 控件以通常方式添加到窗口并显示。结果是，加载的图像将神奇地出现在窗口中。

## 两个窗口之间的交互

我之前提到过像 `ImageViewer` 这样的应用程序的问题之一，是主窗口菜单、工具栏按钮与图像窗口本身之间的交互。`ImageViewer` 允许用户打开任意数量的图像，因此不仅需要一种方法让主窗口确定与哪个窗口交互，还需要一种方法让图像窗口跟踪它们自己的数据。

```c
/* 获取活动窗口 */
window = GetActiveWindow();

/* 在继续操作之前检查活动窗口是否有效 */
if ( window != NULL ) {
    /* 获取活动图像 */
    image = GetActiveImage();

    /* 旋转图像 - 第二参数目前被忽略 */
    gdk_imlib_rotate_image ( image, 0 );

    /*将新图像放入窗口 */
    SetImageIntoWindow ( window, image );
}
```

`imagewerutility` 并没有直接暴露 `lastwindow` 和 `lastimage` 指针，而是暴露了两个函数，它们返回相应的指针值——`GetActiveWindow` 和 `GetActiveImage`。`Rotate` 函数执行的第一件事是获取活动窗口指针并检查它是否不为 `NULL`。只要它有一个有效值，我们就可以确定在点击工具栏上的旋转按钮之前，已经选择了一个图像。此时，代码就可以开始工作了。

调用 `GetActiveImage` 是为了确定窗口中显示的图像指针。然后，该指针被传递给函数 `gdk_imlib_rotate_image` 来旋转图像。最后，调用 `SetImageIntoWindow` 并同时传入窗口和图像指针，让新旋转的图像魔法般地出现。这并不难，对吧？（顺带一提，GDK 在图像旋转时会对其进行镜像，这是 `gdk_imlib_rotate_image` 的一个小缺陷）。

![](img/aa3546013f120531cd191b770d85869c_494_0.png)

图像翻转的工作原理类似。当按下任一个 `Flip`（翻转）按钮时，会调用 `mainwindow` 中的 `FlipHandler`。

```c
void FlipHandler ( GtkButton * button, gpointer data ) {
    if ( GPOINTER_TO_INT ( data ) == 0 )
        FlipImage ( TRUE );
    else
        FlipImage ( FALSE );
}
```

# 第18 章

同样来看看这两个工具栏按钮的定义。

```c
{GNOME_APP_UI_ITEM, "Flip", "水平翻转图像", FlipHandler,
GINT_TO_POINTER (0), NULL,
GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_BACK),
{GNOME_APP_UI_ITEM, "Flip", "垂直翻转图像", FlipHandler,
GINT_TO_POINTER (1), NULL,
GNOME_APP_PIXMAP_STOCK, GNOME_STOCK_PIXMAP_DOWN),
}
```

同一个处理程序被用于图像的水平和垂直翻转。在水平翻转的情况下，将整数值 0 传递给 `data` 参数，而垂直翻转时则将值 1 传递给处理程序。现在，记住，任何回调函数的 `data` 参数都是指针，而不是整数。GTK+ 提供了一些实用的宏，允许你将整数而不是指针作为 `data` 参数传递。`GINT_TO_POINTER` 函数将整数值转换为值值，而 `GPOINTER_TO_INT` 将指针值转换回整数。
