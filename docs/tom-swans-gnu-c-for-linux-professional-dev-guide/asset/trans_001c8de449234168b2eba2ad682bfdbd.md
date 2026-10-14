

## 响应键盘事件

示例程序的事件循环演示了如何响应 KeyPress 事件并查找其符号值。为此，我们需要声明如下几个变量：

```
KeySym key;
XComposeStatus cstat;
int size = 32;
char keyname[size];
keyname[0] = 0;
```

KeySym 变量等同于 keysymdef.h 中定义的 XK_ 符号。本程序未使用 XComposeStatus，它仅在带有 Compose 键或类似名称键（用于选择备用字符集）的系统上才有意义。这类键可能出现在支持多种语言的桌面出版系统等计算机上，或者因其他目的需要特殊符号的计算机上。大多数情况下，你可以忽略 XComposeStatus 值，但为了下一个要介绍的键映射查找函数 XLookupString()，你仍然必须定义它。

## 映射键盘事件代码

XLookupString() 函数接受多个参数，并返回两个重要值：一个等于事件键码名称的字符串，以及该键的符号值。切勿直接使用事件的键码值。为确保可移植性，所有键值都必须通过调用 XLookupString() 获取。该函数会查询 X 服务器中针对用户硬件的键映射表。请记住，你的客户端可能会被多个运行在不同硬件上的服务器共享。如果直接使用事件的键码，你的程序几乎肯定会失败。在响应 KeyPress 或 KeyRelease 事件时，按如下方式调用 XLookupString()：

```
XLookupString(&event.xkey, keyname, size, &key, &cstat);
```

第一个参数引用 X 联合体，该联合体提供了特定于 KeyPress 或 KeyRelease 事件对象的字段。接下来是一个指向 char 缓冲区的指针 keyname，后面跟着该缓冲区的大小（以字节为单位）。函数会将键的字符串名称复制到此缓冲区中。大多数键名只有一个字符长——例如，XK_A 键的名称是字符串 "A"。但是，根据所使用的服务器，功能键和其他键的名称可能更长。

传递给 XLookupString() 的最后两个参数是 KeySym 和 XComposeStatus 变量的地址。函数会将事件键码的符号值赋给 KeySym 变量。如前所述，XComposeStatus 值被忽略。

![](img/6eab91cc30158075ed10d0cabbac9029_698_0.png)

查找键的名称和符号值后，你可以使用它来显示文本或选择程序功能。示例程序两者都做了。它调用一个本地函数 ShowKey() 来以十进制显示键的名称和符号值。在调用 XLookupString() 之后，返回的 KeySym 值可以与 keysymdef.h 中的任何 XK_ 常量进行比较。示例程序使用这种技术来检测 Esc 键，并在你按下该键时结束事件循环：

```
if (key == XK_Escape)
    done = true;  // Exit on escape key
```

> 提示
> 当你不需要键的字符串名称时，可以调用 XLookupKeysym() 函数来获取其符号值。下一节中的示例程序演示了如何使用此函数。

## 窗口属性

窗口的属性指定了各种显示特性，例如背景和前景颜色、光标形状以及边框宽度。设置窗口属性有三种方式：

- 创建时通过调用 XCreateWindow()
- 创建后通过调用 XSetWindowBorder() 和类似的实用函数
- 创建后通过调用 XChangeWindowAttributes()

在大多数情况下，客户端在创建 Window 结构时选择窗口的属性，但你始终可以在之后更改任何属性。但请记住，每次这样的更改都会导致网络流量增加。为了获得最佳效果，请在首次创建新窗口时尽可能多地指定属性。接下来的三节将分别展示三种窗口属性技术的示例。

> 提示
> 你可以自由使用此处描述的任何方法在创建后更改窗口属性。由于 Xlib 会将所有此类技术合并为单个网络请求，因此在网络性能影响方面，没有哪种方法比另一种更高效。

## 使用属性创建窗口

若要在创建窗口时指定属性，请在连接到 X 服务器后执行以下一般步骤：

- 1. 声明一个 Xlib XSetWindowAttributes 结构的变量。
- 2. 为该结构的字段赋值。

