
# GNOME 2 开发者官方指南

/* -*- utf-8; -*- */

如果你的程序包含重音符号或其他非 7 位 ASCII 字符，这个 UTF-8 指示就非常重要。大多数 GTK+ 和 GNOME 程序都使用 7 位 ASCII。你可以添加其他语言的翻译；见第 6.5 。

### 3.1.4 组件基础

所有的 GTK+ 组件都是 `GtkWidget`（类型标识符：`GTK_TYPE_WIDGET`）对象，因此它们是 `GObject` 类（所有 GTK+ 类的基类）的成员。

`GObject` 组件的一个特殊之处在于引用计数机制与普通 `GObject` 对象略有不同。新创建的组件有一个浮动引用，当你将组件放入容器时，容器会接管该引用。这确保了 GTK+ 在容器删除时清理组件，不需要在你的代码中移除额外的引用。

基础 `GtkWidget` 类包含了可见的操作元素（方法、属性和信号）。后续章节将概述最重要的部分。

### 3.1.5 方法

显示一个组件：

```
GtkWidget *widget;

gtk_widget_show(widget);
```

然而，更实用的方法是使用

```
gtk_widget_show_all(widget)
```

为了显示组件并执行任何更改其外观的操作，GTK+ 不会立即更改组件；相反，它等待程序进入主循环。如果微秒级的差异对你来说确实很重要，请调用

```
gtk_widget_show_now(widget);
```

警告 调用 `gtk_widget_show_now()` 等同于运行主循环，在此期间 GTK+ 可以处理与当前组件未请求的事件并抛出信号。

显示组件的反面是隐藏组件；使用以下两种方法之一：

```
gtk_widget_hide(widget)
gtk_widget_hide_all(widget)
```

要彻底删除一个组件，

```
gtk_widget_destroy(widget)
```

部件的销毁是书中几个示例中的重要部分。

### 3.1.6 属性

最重要的布尔属性有：

- `visible`: 如果部件可见的，则为 TRUE。
- `sensitive`: 如果部件处于未激活状态（变灰），则为 FALSE。在未激活状态下，部件对输入没有响应。
- `can-focus`: 如果部件可以获取输入，则为 TRUE。
- `has-focus`: 如果部件已获得输入焦点，则为 TRUE。
- `can-default`: 如果允许部件成为其窗口的默认焦点，则为 TRUE。
- `has-default`: 如果部件是其窗口的默认部件，则为 TRUE。
- `receives-default`: 如果窗口在获得焦点时该部件成为默认部件，则为 TRUE。

默认部件在窗口打开后接收输入，因此它应该是“危险性”最小的部件之一。在对话框中，通常位于右下角。默认部件的目的是实现更好的键盘操作；例如，用户可以通过按下 ENTER 键来操作对话框上的按钮。

### 3.1.7 信号

`GtkWidget` 对象有许多关联信号；大多数应用程序忽略了其中的绝大多数。这里是三个最实用的信号，以及它们的处理器原型：

```
boolean handler(GtkWidget *widget, GdkEvent *event, gpointer data)
```

对于窗口来说这是一个重要的信号，因为 GTK 在窗口想要销毁部件时发射此信号（例如，当你点击标题栏中的按钮时）。对于其他事件信号，处理器通过事件参数获取实际事件。你可以安全地忽略事件。如果你希望信号发射立即停止，你的处理器应该返回 TRUE。

- `show`

```
void handler(GtkWidget *widget, gpointer data)
```

当部件变为可见时，GTK+ 会发射此信号。

- `hide`

```
void handler(GtkWidget *widget, gpointer data)
```

当部件被隐藏时，GTK+ 会发射此信号。

# GNOME 开发者官方指南

## 3.2 窗口

在节 3.1.3 的示例程序中有一个窗口，你可以看到它是一个 `GtkWindow` 类的容器部件对象（类型标识符：`GTK_TYPE_WINDOW`）。

要设置窗口标题，请向其标题属性写入一个字符串。用户应该能够在窗口列表（例如，在窗口管理器中）区分窗口标题。应用程序窗口的标题理想情况下源自该窗口中当前打开的文档文件名、目录或类似内容。如果你坚持在标题中包含应用程序名称，请将其放在文档名称之后，但 GNOME 指南建议不要这样做。标题栏中的任何其他信息在本质上都是浪费空间。

以下是相同标题的几个版本及其排名：

- 良好：`Order.mtx`
- 尚可：`Order.mtx` - MiracleText
- 差：MiracleText: `Order.mtx`
- 极其糟糕：MiracleText 0.16.7 (CVS BUILD #1247)

如果窗口不包含文档，则以下约定有所不同：

- 应用程序窗口：应用程序名称（LavaLamp）。
- 属性窗口：对象名称 - 属性（表 3.1 - 属性）。
- 偏好窗口：应用程序名称 – 偏好（MiracleText - 偏好）。
- 警告：否；包含警告的窗口将以短消息的形式在窗口内显示其信息；如果你把相同的内容放在标题栏中，它会在屏幕上显示两次，看起来会有点混乱。好吧，至少指南是这么说的。我的观点是，像 Warning 或 Info 这样的短标题永远不会伤害任何人。此外，窗口在窗口管理器的列表中看起来有点老旧。第 3.10 节涵盖了对话框以及 GTK+ 可能自动提供的标题。
- 灵（助手）：小灵的名称（Configure Coffee Machine）；更多详细信息请参见第 4.3.15 节。

重要的 `GtkWindow` 属性及其类型包括：

- `resizable` (布尔)：如果为 TRUE，用户可以更改窗口大小。

注意：将此属性设置为 FALSE 不是一个好主意，这使得使用户无法根据偏好调整窗口。如果你正确使用容器层，内容在任何大小下都能保持可用性且顺序正确。

- `modal` (布尔)：当为 TRUE 时，这是一个模态窗口。只要该窗口存在，应用程序的其他窗口就不会对输入做出响应。

警告：在大多数现代应用程序中，模态窗口完全没有必要。你应该尝试不使用模态窗口，因为当窗口由于某些隐藏的对话框而忽略用户的输入时，用户往往会感到沮丧。

- `window-position` (`GtkWindowPosition`)：此属性决定窗口在显示器上的出现位置。可能的值有：

- `GTK_POS_NONE`：让窗口管理器决定将其放在哪里。这是默认值。
- `GTK_POS_CENTER_ON_PARENT`：将窗口放在父窗口上方，使用父窗口的中心作为其中心。
- `GTK_POS_CENTER`：将窗口放在显示器的中心，尽可能如此。
- `GTK_POS_CENTER_ALWAYS`：尝试保持窗口居中，即使窗口大小发生变化。
- `GTK_POS_MOUSE`：将窗口尽可能靠近鼠标。

- `default-width` (int)：默认宽度。
- `default-height` (int)：默认高度。
- `destroy-with-parent` (布尔)：如果为 TRUE，GTK+ 将销毁窗口。
- `icon` (`GdkPixbuf`)：图标。

- `set_icon_from_file(const char *filename, GError **error)`：从文件名设置图标。
- `set_icon(GtkWindow *window, GdkPixbuf *pixbuf)`：设置图标 pixbuf。
- `set_icon_list(GtkWindow *window, GList *pixmap)`：设置所有图标。

## 3.3 显示部件

在最基础的部件中，显示部件仅向用户展示某些内容，例如文本、图片和进度。

- `Label`：描述相邻部件的短文本。Pango 让标签格式化变得简单。标签不适用于大量文本；替代方案请参见第 12 节中的文本缓冲区和视图部件。
- `Image`：在屏幕上显示图片。此类部件与 `GdkPixbuf` 配合工作，GDK 接口允许你加载和显示几乎常见格式的图像文件。
- `Progress bar`：向用户展示应用程序执行特定任务的具体进展。进度条可以显示应用程序执行了多少。如果应用程序不知道操作需要多长时间，进度条可以进入活动模式以显示正在进行（这看起来有点像《星际战士》中的殖号）。

第 3.3.3 节包含更多关于进度条的信息。

# GNOME 官方开发者指南

接下来是主程序。许多主声明，如 `gtk_init()`、主窗口的创建以及其销毁信号处理器的绑定，都在这里：

```c
int main(int argc, char **argv) {

  GtkWindow *window;

  GtkBox *vbox;

  GtkLabel *label, *label_markup;

  GtkImage *image;

  GtkBox *progress_bar;
```
