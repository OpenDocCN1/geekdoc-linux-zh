
```c
void OnSwitchPage(GtkNotebook* notebook, GtkNotebookPage* page, int page_num)
{
    GtkWidget* child;
    GtkWidget* tabLabel;
    char* pageName;

    /*获取页面名称*/
    child = gtk_notebook_get_nth_page(notebook, page_num);
    tabLabel = gtk_notebook_get_tab_label(notebook, child);
    gtk_label_get(GTK_LABEL(tabLabel), &pageName);

    /*打印信息*/
    g_print("Switched to page %d\n", page_num);
    g_print("New page's name is %s\n", pageName);

    g_print("\n");
}

int main(int argc, char** argv)
{
    GtkWidget* notebook;

    /*连接到笔记本的 "switch-page" 信号*/
    gtk_signal_connect(GTK_OBJECT(notebook), "switch-page",
                        GTK_SIGNAL_FUNC(OnSwitchPage), (gpointer)notebook);
}
```

![](img/7fa9959a9d28ad339fa75e44952feeb9_534_0.png)

笔记本在 `main()` 中创建（第 23 行，未显示），然后在第 26 行使用 `gtk_signal_connect()` 以通常方式将其 `switch-page` 信号连接到 `OnSwitchPage()`。笔记本的指针作为最后一个参数传递给 `gtk_signal_connect()`，以便它可以在 `OnSwitchPage()` 中作为第四参数可用。每当笔记本中的当前页面更改时，就会调用 `OnSwitchPage()` 函数。当调用它时，它执行的第一件事是使用 `gtk_notebook_get_nth_page()`（第 9 行）获取当前页面组件的指针。该指针用于使用 `gtk_notebook_get_tab_label()`（第 10 行）获取页面标签的指针，而标签指针用于使用 `gtk_label_get()`（第 11 行）获取当前显示在标签上的文本。最后，作为 `page_num` 参数传递给函数的页码以及来自标签页的文本通过 `g_print()` 输出到终端；该程序是从 `notebook.c` 的第 14-16 行启动的。`notebook.c` 中的窗口如图 18.5 所示。

## 图 18.5

![](img/7fa9959a9d28ad339fa75e44952feeb9_535_0.png)

笔记本部件示例。

## 总结

今天你学习了四种容器部件以及如何使用它们来管理用户界面中的其他部件。你学习了如何使用固定布局部件（fixed widgets）将部件放置在固定位置，并学习了当你想要按照窗口允许的固定方式布局更多部件时如何使用布局部件（layout widgets）。通过填充部件（padded widget），你学习了如何将两个部件并排放置，以便用户可以在它们之间分配它们所占据的空间。最后，你使用了笔记本部件（notebook widgets）让部件在你的用户界面上共享相同的空间。明智地使用这些部件可以使用户的界面对用户更容易管理，但滥用它们会让用户对你界面的体验变得非常糟糕。

# 更多容器部件

## 问答

固定部件（fixed widget）有什么缺点？为什么我不经常看到使用它们？

该部件的子元素是“固定的”，它们不会随着父容器大小的变化而调整大小或移动。如果用户调整了固定部件父容器的大小，可能会导致界面布局问题。通过为你的应用程序设置顶层窗口的策略，不允许用户调整固定部件父容器的大小，可以避免这个问题。然后你又遇到另一个问题：用户的屏幕并不相同，也不是以相同的分辨率运行。在 1152x768 下工作良好良好的界面，在 640x480 下可能完全无法使用。为了解决这个困境，你可以在启动时固定应用程序的大小。但此时你基本上是在重新实现一个不具备缩放功能的 `GtkBox` 或 `GtkTable`。如这些所示，大多数情况下使用固定部件得不偿失。唯一真正增加的功能是可以移动部件，但极少数应用程序需要此功能。

如果我需要显示一个大的位图（pixmap）或其他倾向于变得很大的部件（例如 `GtkList`），我应该把它放在布局部件中吗？

这是处理大部件的一种方法，但你必须确保实现滚动条来控制布局部件。对于列表，你还需要监控列表的大小，并确保布局部件的滚动区域足够容纳它。通常情况下，更好的解决方案是使用 `ScrolledWindow`，它会自动处理所有这些。你明天将学习这些部件。

我有许多按钮。事实上，当窗口大小合理时，按钮多到无法放进窗口内。我不想把按钮弄得非常小以便让它们放进窗口。这是一个使用布局部件的好时机

如果你能根据按钮的功能将它们分成不同的类别，那么笔记本部件（notebook widget）将是一个好得解决方案。每个类别的按钮都可以有自己的页面，并在页面上放置这些按钮。即使你不能将它们分类，你的用户使用笔记本部件的体验可能会更好。

在寻找按钮时，切换页面比在周围滚动要容易得多。

Q：我经常看到应用程序在 notebook 页面中包含多个小部件（widgets），在之前的回答中，你建议在每个 notebook 页面中放置多个按钮。如果一个 notebook 页面只能包含一个 widget，我该如何将所有 widget 放入一个 notebook 页面呢？

A：记住，你可以将任何类型的 widget 封装到容器 widget 中；这包括其他容器 widget。因此，你不需要直接将 widget 放在 notebook 页面中。相反，你应该在 notebook 页面中放置另一个容器 widget（例如框或表格），然后将其他 widget 放入该容器。这对于分格部件（paned widgets）也有效，每个窗格只能包含一个 widget。虽然在一个窗格中放置多个 widget 的情况很少见，但可以通过在窗格中放置另一个容器 widget，然后将其他 widget 放入容器来实现。这种做法并不常见，因为分格 widget 在每个窗格包含多个 widget 时工作效果不好，看起来也不太好看。

## 工作坊

提供测验和练习部分是为了让你测试对今天所学知识的掌握情况。答案位于录 A。“答案”。练习将让你获得使用今天所学知识的实践经验。

## 测验

1. 什么决定了固定 widget（fixed widget）的大小？

2. 如果你在固定 widget 上放置一个 widget，其位置导致 widget 的部分超出边缘，会发生什么？

3. 什么决定了布局 widget 可滚动区域的大小？什么决定了它在屏幕上的尺寸？

4. 如何控制布局 widget 的滚动？

5. 为什么 `paned.c` 中的右侧窗格有一个最小尺寸？

6. 如果将 `paned.c` 中的窗口缩小到右侧窗格处于其最小尺寸的程度，会发生什么？

7. 如果一个 notebook widget 的页面过多，以至于标签（tabs）无法全部沿 notebook 边缘对齐，会发生什么？

8. 你的程序如何知道 notebook 窗口中的当前页面何时发生了变化？

## 练习

1. 这段代码有什么问题？

```c
GtkWidget* fixed;
GtkWidget* button;

fixed = gtk_fixed_new();
button = gtk_button_new_with_label("Button");
gtk_fixed_move(GTK_FIXED(fixed), button, 50, 50);
```

2. 修改 `layout.c`，使得布局 widget 在创建时设置为使用滚动条的调整对象（adjustment objects）。

3. 在 `layout.c` 的 layout widget 中添加更多 widget，并让它们在点击按钮时改变位置。

4. 为什么以下代码无法按预期方式工作？

```c
GtkWidget* pared;
GtkWidget* label1;
GtkWidget* label2;

pared = gtk_paned_new();
label1 = gtk_label_new("Pane 1");
label2 = gtk_label_new("Pane 2");
```

```c
gtk_paned_pack1(GTK_PANED(pared), label1, FALSE, TRUE);
gtk_paned_pack2(GTK_PANED(pared), label2, FALSE, FALSE);
```
