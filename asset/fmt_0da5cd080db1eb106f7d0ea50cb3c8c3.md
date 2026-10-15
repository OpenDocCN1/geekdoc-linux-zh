
```c
if (keyboard_keypressed(SCANCODE_ENTER)) {
    /* 执行某个事件 */
}
```

请注意，只有当你偶尔调用`keyboard_update()`或`keyboard_waitforupdate()`时，键盘事件才会被处理。

`keyboard_translatekeys()`还允许某些重新映射操作。这使得具有多个物理键的键（即数字数字和`Enter`）可以显示在相同的扫描码下。

> **注意**：`#define`实例的名称源自美国键盘布局。当使用来自其他国家的键盘时，定义将指的是位于相同物理位置的键，但键帽上的标识会有所不同。

以下是支持的扫描码：`SCANCODE_0`到`SCANCODE_9`、`SCANCODE_KEYPAD0`到`SCANCODE_KEYPAD9`、`SCANCODE_A`到`SCANCODE_Z`、`SCANCODE_F1`到`SCANCODE_F12`、`ESCAPE`、`MINUS`、`EQUAL`、`BACKSPACE`、`TAB`、`BRACKET_LEFT`、`BRACKET_RIGHT`、`ENTER`、`LEFTCTRL`、`SEMICOLON`、`APOSTROPHE`、`GRAVE`、`LEFTSHIFT`、`BACKSLASH`、`COMMA`、`PERIOD`、`SLASH`、`RIGHTSHIFT`、`KEYPADMULTIPLY`、`LEFTALT`、`SPACE`、`CAPSLOCK`、`NUMLOCK`、`SCROLLLOCK`、`CURSORUPLEFT`、`CURSORUPRIGHT`、`CURSORLEFT`、`CURSORRIGHT`、`KEYPADMINUS`、`CURSORDOWNLEFT`、`CURSORDOWN`、`CURSORDOWNRIGHT`、`KEYPAD_PERIOD`、`LESS`、`KEYPADENTER`、`RIGHTCONTROL`、`CONTROL`、`KEYPADDIVIDE`、`PRINTSCREEN`、`RIGHTALT`、`BREAK`、`ALTERNATE`、`HOME`、`CURSORBLOCKUP`、`PAGEUP`、`CURSORBLOCKLEFT`、`CURSORBLOCKRIGHT`、`END`、`CURSORBLOCKDOWN`、`PAGEDOWN`、`INSERT`以及`REMOVE`。

### `char *keyboard_getstate(void)`

在原始键盘模式下，此例程返回指向静态缓冲区的指针。如果`buffer[scancode]`中的值是`KEY_PRESSED`或`KEY_NOT_PRESSED`，你也就知道了是否按下。

#### 关键状态

如果具有该扫描码的按键已被按下，则`buffer[SCANCODE]`的值为`1`。实际上，`KEY_PRESSED`为`1`，`KEY_NOT_PRESSED`为`0`，这使得你可以使用类似以下的结构：

```c
if (buffer[SCANCODE_ENTER]) {
    /* do something */
}
```

如果你需要检查许多不同的按键，这种方式比调用`keyboard_keypressed()`更高效。请注意，只有在你偶尔调用`keyboard_update()`或`keyboard_waitforupdate()`时，键盘事件才会被处理。

### `void keyboard_clearstate(void)`

在原始键盘模式下，`SVGLib`从内核接收按键按下和释放事件，并跟踪当前哪些按键处于按下状态。调用`keyboard_clearstate()`会将此信息设置为所有按键释放。你可以在程序中的特定位置使用它进行清理。此外，当发生虚拟控制台（VC）切换时，`SVGLib`会重置所有按键的状态，因为它在重新获取控制台控制权时不知道按键的当前状态。

```c
typedef void (*_keyboard_handler) (int scancode, int press);

void keyboard_seteventhandler(_keyboard_handler handler)
```

参见`keyboard_setdefaulteventhandler()`。

### `void keyboard_setdefaulteventhandler(void)`

这些函数允许你定义一个键盘事件处理程序，该处理程序在发生键盘事件时由`keyboard_update()`和`keyboard_waitforupdate()`调用。参数`press`在按键扫描码被释放或按下时分别为`KEY_EVENTRELEASE`或`KEY_EVENTPRESS`。实际上，第一个值为`0`，第二个值为`1`（这种设计很直观，方便你在程序中使用）。即使你指定了自己的处理程序，`SVGLib`仍会检查`Alt+F7`或`Ctrl+C`以进行控制台切换或生成`SIGINT`信号（如果`keyboard_translatekeys()`允许这样做）。

调用`keyboard_setdefaulteventhandler()`会恢复默认处理程序，该程序维护`keyboard_getstate()`和`keyboard_keypressed()`所使用的表。在重新启用默认处理程序后，调用`keyboard_clearstate()`可能是一个好主意。有关扫描码列表，请参见`keyboard_keypressed()`。

## 操纵杆处理

本节的函数涵盖了操纵杆处理：

> **注意**
> 这些函数必须包含`<vgajoystick.h>`。操纵杆模块基本上独立于`SVGLib`的其他部分。你可以轻松地在纯文本模式下使用它，但这样做没有好处。然而，如果在图形模式下使用，它会在VC切换时释放操纵杆设备，以便多个应用程序可以共享操纵杆。不幸的是，这在操纵杆校准期间不起作用。因此，在图形模式下校准时，你应该使用`vgalockvc()`锁定VC。此外，如果仅在文本模式下使用操纵杆，`SVGAlib`无法检测VC切换，且操纵杆不能在应用程序之间共享。

简单的测试`demo joytest()`和更复杂的图形`mjoytest()`演示以越来越多的细节展示了操纵杆包的使用。

这些函数仅在`SVGAlib`的`ELF`版本中可用（大多数用户使用的就是这种版本）。由于向后兼容性问题，它不能与共享的`.a`外部库一起使用。某些游戏移植版本似乎无法正确检测缺失的操纵杆。（这也可能是Linux设备驱动程序的问题。）无论如何，在使用操纵杆接口时，请允许你的应用程序用户指定要使用的操纵杆数量，以及退出操纵杆校准（当他们无法按下缺失操纵杆上的按钮时）。通常`Ctrl+C`有效，但你不应该过度依赖它，因为它可能被禁用。作为一个通用准则，请尝试在仍处于文本模式时打开并校准操纵杆。此时`Ctrl+C`通常仍然有效。如果成功，你可以假设在任何后续的图形模式重新校准中操纵杆都存在。

```c
typedef void (*_joystick_output)(const char *msg);

int joystick_init(int joydev, _joystick_output jo)
```

此函数打开一个操纵杆设备。如果失败，则返回负值——否则操纵杆已初始化。`SVGAlib`支持多个操纵杆。相应的设备代码名称可以在`/etc/vga/libvga.config`中配置。

`joydev`参数指示要初始化哪个操纵杆。截至本文撰写时，`SVGAlib`最多支持四个操纵杆：`joydev = 0`到`joydev = 3`。但请注意，现有的硬件和内核驱动程序可能只能处理操纵杆`0`和`1`。

强烈建议你的程序允许用户校准操纵杆。这是由`jo`参数控制的。如果它为`NULL`，则不进行校准。否则，将执行校准，并通过调用用户提供的`jo`函数向用户打印说明。该函数的职责是向用户打印`NUL`和`NL`结尾的消息（由`msg`指向）。消息可能包含嵌入式`NL`字符，且长度不超过`256`个字符（包括终止符`NUL`）。

通常`fputs(msg, stdout);`后接`fflush(stdout);`即可，但为了方便，你可以通过为`jo`传递`JOY_CALIB_STDOUT`来执行相同操作。`gl_printf()`也非常适合此任务。然而，它需要先进行一些字体设置，因此没有提供特殊的预处理器常量。

初始化一个已初始化的操纵杆是有效的。这允许你随时重新校准操纵杆。该模块支持旧版本`0.x`以及新版本`1.x`操纵杆设备协议。

```c
void joystick_close(int joydev)
```
