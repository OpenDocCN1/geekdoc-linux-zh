
```c
1: Widget create_canvas( Widget parent )
2: {
3:     GxObjPtr gx_obj;
4:
5:     if ( gxObjHeader == NULL ) {
6:         gxObjHeader = obj;
7:     } else {
8:         gx_obj = gxObjHeader;
9:
10:         /* find the end of the object list */
11:         while ( gx_obj->next != NULL ) {
12:             gx_obj = gx_obj->next;
13:         }
14:
15:         /*
16:          * add the new object to the end of our list
17:         */
18:         gx_obj->next = obj;
19:     }
20:
21:     gx_obj->action = NULL;
22:     gx_obj->next = NULL;
23:
24:     draw_mgr_func = NULL;
25:
26:     return gx_obj;
27: }
```

为了使填充行为能够正常工作，必须首先使用列表 17.5 所示的 `grid_bits` 位图数据创建一个位图。

### 列表 17.5 grid.xbm 文件的内容

```
1: #define grid_width 10
2: #define grid_height 10
3: static unsigned char grid_bits[] = {
4: 0x00,0x00,0x00,0x00,0x49,0x02,0x00,0x00,0x00,
5: 0x00,0x02,0x00,0x00,0x00,0x00,0x02,0x00,0x00};
```

为了语法语法正确并防止与列表 17.4 所示更改相关的编译错误，你必须根据列表 17.5 创建 `grid.xbm` 文件，并将其放在 `src/include` 目录下。

此外，必须在 `gxGraphics.c` 的开头添加 `grid.xbm` 文件的包含指令，如下：

最后，必须在 `gxGraphic.h` 头文件的 GLOBAL 部分添加以下行：

```
GLOBAL Pixmap GxDrawAreaBG;
```

# 使用光标作为状态指示

X窗口环境的默认光标是左箭头光标。这用于正常操作，但可以更改以反映应用程序可能进入的任何状态。

基于 X 的应用程序可用的光标可以在 `cursorfronts.h` 中。列表 17.6 显示了根据应用程序已的光标模式更改光标的图形编辑器实用程序。

### 列表 17.6 要添加到 gxGraphics.c 的 set_cursor 函数源代码

```c
1: void set_cursor(CursorMode mode )
2: {
3:   Cursor new_cursor;
4:
5:   switch (mode) {
6:     case LINE_MODE:
7:       new_cursor = gxCrosshair;
8:       break;
9:
10:    case PENCIL_MODE:
11:      new_cursor = gxPencil;
12:      break;
13:
14:    case EDIT_MODE:
15:      new_cursor = gxEdit;
16:      break;
17:
18:    case TEXT_MODE:
19:      new_cursor = gxTextI;
20:      break;
21:
22:    case SCALE_MODE:
23:      new_cursor = gxScale;
24:      break;
25:
26:    case MOVE_MODE:
27:      new_cursor = gxMove;
28:      break;
29:
30:    case NORMAL_MODE:
31:      default:
32:        new_cursor = gxNormal;
33:        break;
34:  }
35:  XDefine(XtDisplay(gxDrawArea),
36:  XtWindow(gxDrawArea),new_cursor);
37:  XFlush(XtDisplay(gxDrawArea));
38: }
```

`set_cursor` 函数所需的参数数据类型为 `CursorMode`。这是图形编辑器（Graphics Editor）特有的数据类型，定义为如列表 17.7 所示的枚举类型。

### 列表 17.7 包含在 gxGraphics.h 头文件中的 CursorMode 枚举

```c
1: typedef enum _cursor_mode {
2:   NORMAL_MODE = 0,
3:   PENCIL_MODE,
4:   EDIT_MODE,
5:   TEXT_MODE,
6:   MOVE_MODE,
7:   SCALE_MODE,
8:   LINE_MODE,
9: } CursorMode;
```

`set_cursor` 函数根据传递给函数的指定的 `CursorMode` 值进行切换，并将 `new_cursor` 值设置为列表 17.8 所示的全局变量之一。

### 列表 17.8 包含在 gxGraphics.c 源文件中的全局光标引用

- 1: `Cursor` `gxCrosshair`;

- 2: `Cursor` `gxPencil`;

- 3: `Cursor` `gxEdit`;

- 4: `Cursor` `gxNormal`;

- 5: `Cursor` `gxText`;

- 6: `Cursor` `gxMove`;

- 7: `Cursor` `gxScale`;

在确定了 `new_cursor` 值后，将为 `GxDrawArea` 控件的窗口定义对应的光标值：

```c
35: XDefineCursor(XtDisplay(GxDrawArea),
36: XtWindow(GxDrawArea), new_cursor );
```

并将由 `XDefineCursor` 函数生成的 expose 事件从应用程序事件队列中刷新，以确保新光标立即显示在绘制区域中。

```c
37: XFlush(XtDisplay(GxDrawArea) );
```

列表 17.8 所示的 `Cursor` 变量需要在应用程序调用之前准备好值，因此在 `gxGraphics.c` 源文件中添加了一个名为 `initializeGX` 的新函数。

`initializeGX` 函数的内容见列表 17.9。该函数的目的是初始化除列表 17.8 所示的光标变量外，应用程序所使用的所有全局变量。

### 列表 17.9 用于 gxGraphics.c 文件的 initializeGX 函数源代码

| 行号 | 代码 |
| :--- | :--- |
| 1 | `void initializeGX( void )` |
| 2 | `{` |
| 3 | `Pixel color;` |
| 4 | `Display *dsp = Xtdplay(GxDrawArea);` |
| 5 |  |
| 6 | `XtVaValues(GxStatusBar, Xnbackground, &color, NULL );` |
| 7 |  |
| 8 | `gxObjHeader = NULL;` |
| 9 | `gxObjCurrent = NULL;` |
| 10 |  |
| 11 | `gxCrosshair = XCreateCursor(dsp, XC_crosshair);` |
| 12 | `gxPencil = XCreateCursor(dsp, XC_pencil);` |
| 13 | `gxEdit = XCreateCursor(dsp, XC_cross);` |
| 14 | `gxTextI = XCreateCursor(dsp, XC_xterm);` |
| 15 | `gxScale = XCreateCursor(dsp, XC_dtbox);` |
| 16 | `gxmove = XCreateCursor(dsp, XC_hand1);` |
| 17 | `gxNormal = XCreateCursor(dsp, XC_top_left_arrow);` |
| 18 |  |
| 19 | `rubberGC = XCreateGC(Xtdplay(GxDrawArea), rubberGC, color );` |
| 20 | `DefaultRootWindow(Xtdplay(GxDrawArea), 0, NULL );` |
