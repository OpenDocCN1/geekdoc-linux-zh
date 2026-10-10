

[PAGE 416] 的正文内容如下：

```c
157         case GDK_Alt_R:
158             altKeyDown = FALSE;
159             break;
160         case GDK_Control_L:
161         case GDK_Control_R:
162             controlKeyDown = FALSE;
163             break;
164         case GDK_Meta_L:
165         case GDK_Meta_R:
166             metaKeyDown = FALSE;
167             break;
168         case GDK_Shift_L:
169             leftShiftKeyDown = FALSE;
170             break;
171         case GDK_Shift_R:
172             rightShiftKeyDown = FALSE;
173             break;
174     }
175     return(TRUE);
176 }
177 
178 gint eventDelete(GtkWidget *widget,
179                 GdkEvent *event,gpointer data) {
180     return(FALSE);
181 }
182 
183 gint eventDestroy(GtkWidget *widget,
184                 GdkEvent *event,gpointer data) {
185     gtk_main_quit();
186     return(0);
187 }
```

我们在应用程序主窗口上连接的事件位于第 35 行到第 51 行。为了判断窗口是否拥有焦点，第 39 行到第 44 行将回调函数 `eventFocus()` 连接到窗口，使得每当焦点进入或离开窗口时该函数都会被调用。第 45 行对 `gtk_signal_connect()` 的调用将回调函数 `eventPressKey()` 赋值，使其在每次按键时被调用；而第 48 行对 `gtk_signal_connect()` 的调用将回调函数 `eventReleaseKey()` 赋值，使其在每次释放按键时被调用。但这还不够。此时，除了按键释放回调外，其他功能都正常工作。默认情况下，小部件被设置为接收焦点事件和按键按下事件，但不接收按键释放事件。第 51 行对 `gtk_widget_add_events()` 的调用使用掩码 `GDK_KEY_RELEASE_MASK`，注册窗口以接收按键释放事件并将其传递给有效的已注册回调函数。

第 53 行到第 65 行创建三个标签并将其插入到一个垂直盒中。顶部的标签名为 `keyLabel`，显示最后一次按键的描述。第二个标签名为 `scrollLabel`，从右向左滚动，显示最近的按键序列。第三个标签名为 `focusLabel`，指示主窗口焦点的当前状态。

[PAGE 417] 的正文内容如下：

第 72 行开始的函数 `eventFocus()` 在窗口获得或失去焦点时会被调用。第 77 行的条件语句检查焦点是丢失还是获得，并设置标签文本以反映当前状态。

每当键盘上的一个键被按下时，第 86 行的函数 `eventPressKey()` 会被调用，并携带关于该按键的信息。`GdkEventKey` 事件包含一个名为 `keyval` 的字段，其中包含按键本身的 ID 号。所有特殊键都有各自的代码。ASCII 键代码与 ASCII 字符的值相同。由于键盘硬件的差异以及国际化因素，键代码超过 1,300 种。如果你想查看完整列表，它们定义在头文件 `gdkkeysyms.h` 中。

第 95 行的 `switch` 语句根据其值选择某些特殊键。第 96 行到第 99 行将一个布尔值设置为 `TRUE`，表示 Alt 键已被按下。类似地，在第 100 行到第 107 行，Control 键和 Meta 键的相同指示器也被设置。请注意，这些键中每一个都有两个值（L 和 R），因为键盘上可能存在两个这样的键，而应用程序可能需要知道这两个键中哪一个被按下。第 108 行到第 113 行为左侧和右侧 Shift 键设置独立的指示器。

第 116 行到第 124 行调整在滚动窗口中显示的文本，该窗口显示最近的按键。通过调用第 116 行的 `gtk_keyval_name()`，键值的描述性名称被复制到工作字符串中。如果该字符可显示，则描述仅为该字符本身；否则，它是一个描述该键的单词。第 117 行和第 118 行将空格和键名追加到用于更新标签文本的 `keyList` 字符串中。第 120 行定义的循环在字符串达到最大长度时执行。左侧的字符会被丢弃，以减少字符串长度。在第 124 行，通过调用 `gtk_label_set_text()` 将新字符串放入标签中。实际显示的按键数量取决于描述每个键所需的字符数。

第 126 行到第 147 行创建一个描述该字符信息的字符串。第 126 行通过在从之前调用 `gtk_keyval_name()` 获取的名称前添加 `GDK_` 来开始描述。这种名称形式是用于标识字符的已定义常量（例如，第 95 行的 `switch` 语句）。第 127 行的测试检查该字符是否为可打印的 ASCII 字符，如果是，则将该字符本身添加到描述中。第 131 行到第 134 行确定该字符是否为大写字母。请注意，与标准的 `C islower()` 宏不同，对 `gtk_keyval_is_lower()` 的调用对除大写字母以外的所有字符都返回 `TRUE`。在第 135 行和第 136 行，键值本身以十六进制数形式打印并添加到字符串中。第 137 行到第 146 行检查布尔值以确定是否有特殊键被按住，如果是，则将此信息添加到描述字符串中。第 147 行对 `gtk_label_set_text()` 的调用将新文本插入标签。

[PAGE 418] 的正文内容如下：

第 151 行的回调函数 `eventReleaseKey()` 在释放按键时会被调用。这里需要关注的只有第 95 行的 `switch` 语句检测到被按下的那些键。如果是这些键之一，其相关的布尔值会被设置为 `FALSE`，以表明它不再被按住。

图 12-3 显示了关于最后一次按下的按键的信息，以及其之前几个按键的一些信息。第一行显示当前字符为小写 c。c 的十六进制值为 0x63。此外，当该键被按下时，Control 键正被按住。从中间一行的右端开始，你可以看到最后一个按键是字母 c。在此之前，左 Control 键被按下。直接在那之前，有一个感叹号。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_418_0.png)

**图 12-3**：监测按键操作

## GNOME 的命令行选项

每个 GNOME 应用程序都有一组可用的命令行选项。对 `gnome_init()` 的调用接受 `argc` 和 `argv` 作为参数，并查找某些选项是否存在。你可以通过启动任何应用程序并指定 `help` 或 `?` 来确定该应用程序可用的选项。你可以使用以下简单程序来演示这一点。

```c
/** showoptions.c **/
#include <gnome.h>

int main(int argc, char *argv[]) {
    gnome_init("showoptions", "1.0", argc, argv);
    exit(0);
}
```

这个程序本身没有选项，但 GNOME、GTK+ 和 X 的选项是可用的。要查看所有这些选项，请像这样运行程序：

```bash
showoptions --help | more
```

[PAGE 419] 的正文内容如下：

输出是可用选项的完整列表：

```text
Usage: showoptions [OPTION...]

GNOME Options
--disable-sound Disable sound server usage
--enable-sound Enable sound server usage
--espeaker=HOSTNAME:PORT Host:port on which the sound
server to use is running

Help options
-?, --help Show this help message
--usage Display brief usage message

GTK options
--gdk-debug=FLAGS Gdk debugging flags to set
--gdk-no-debug=FLAGS Gdk debugging flags to unset
--display=DISPLAY X display to use
--sync Make X calls synchronous
--no-xxxshm Don't use X shared
memory extension
--name=NAME Program name as used by
the window manager
--class=CLASS Program class as used by
the window manager
--gxxd-host=HOST
--gxxd-port=PORT
--xim-preedit=STYLE
--xim-status=STYLE
--gtk-debug=FLAGS Gtk+ debugging flags to set
--gtk-no-debug=FLAGS Gtk+ debugging flags to unset
--g-fatal-warnings Make all warnings fatal
--gtk-module=MODULE Load an additional Gtk module

GNOME GUI options
-V, --version

Help options
-?, --help Show this help message
--usage Display brief usage message

Session management options
--sm-client-id=ID Specify session management ID
--sm-config-prefix=PREFIX Specify prefix of saved
configuration
--sm-disable Disable connection to session
manager
```

这些选项在每个 GNOME 应用程序中都可用。例如，要发现本章开头处程序 `mousefollow` 的版本号，命令和响应看起来如下所示：

```bash
$ mousefollow -V
$ Gnome mousefollow 1.0
```

