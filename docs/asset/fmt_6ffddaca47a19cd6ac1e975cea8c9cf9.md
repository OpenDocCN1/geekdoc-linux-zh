
```
20: GLOBAL Widget GxStatusBar;
21: GLOBAL Widget GxDrawArea;
```

后续包含头文件时，对 `GLOBAL` 存在的测试会将 `GLOBAL` 重新定义为关键字 `extern`。

这是一个强大的机制，允许变量被声明并随后执行。第一个包含它的文件负责声明项目使用的所有全局变量。此外，包含操作告知编译器该变量已经声明。

列表 13.3 显示了 `gxProtos.h` 文件的当前内容。随着更多函数在项目中共享，该文件的复杂性也会增加。

## 列表 13.3 gxProtos.h 文件

```
1: /
2: ** 2D 图形编辑器 (2d-gx)
3: ** gxProtos.h
4: **
5: */
```

## 列表 13.3 续

```
6:   #include <X11/Intrinsic.h>
7:   #include "gxIcons.h"
8: 
9:   #ifndef EXTERN
10:  #define EXTERN
11:  #else
12:  #undef EXTERN
13:  #define EXTERN extern
14:  #endif
15: 
16:  /*
17:   * gxGraphics.c 中的创建例
18:  */
19:  EXTERN WIDGET create_canvas ( Widget );
20:  EXTERN void create_status ( Widget, Widget );
21:  EXTERN void create_buttons ( Widget );
22:  EXTERN void drawAreaProc(Widget, XtPointer, XEvent *, Boolean );
23:   
24:  /*
25:      * GxIcons.h 中使用的绘制函数
26:  */
27:  EXTERN void gx_line ( void );
28:  EXTERN void gx_pencil ( void );
29:  EXTERN void gx_arc ( void );
30:  EXTERN void gx_box ( void );
31:  EXTERN void gx_text ( void );
32:  EXTERN void gx_arrow ( void );
33:  EXTERN void gx_line ( void );
34:  EXTERN void gx_copy ( void );
35:  EXTERN void gx_delete ( void );
36:  EXTERN void gx_select ( void );
37:  EXTERN void gx_save ( void );
38:  EXTERN void gx_export ( void );
39:  EXTERN void gx_load ( void );
40:  EXTERN void gx_set ( void );
41:  EXTERN void gx_ctrl ( void );
42:  EXTERN void gx_exit ( void );
43:  EXTERN void gx_manager(Widget, XtPointer );
44:  EXTERN void gx_manager(Widget, XtPointer );
45:  /**
46:  ** end of gxGraphics.h
47:  */
```

## 应用结构第 13 章 273

```c
51: XtNbottom, XawChainBottom,
52: XtNight, XawChainRight,
53: XtNnFrom, vertical,
54: XtNborderWidth,0,
55: NULL);
56: setStatus("2-GX (c)Starry Knight Software - Ready...");
57: }
58: 
/*
 * statusProc
 */
void statusProc(Widget w, XtPointer msg, XEvent *xe, Boolean flag)
{
  if (msg != NULL)
    setStatus(msg );
  else
    setStatus("0");
}
 
/*
 * create_icons
 */
void create_icons(Widget parent, GxIconData *iconData,
void (*callback)(Widget, XtPointer, XtPointer))
{
  Widget btn;
  Pixmap pix;
 
  while(iconData->info->bits != NULL) 
  {
    if (iconData->info->bits != NULL)
      pix = create_pixmap(parent, iconData->info);
 
    btn = XtCreateManagedWidget(**,
      commandWidgetClass, class,
      XtNwidth, iconData->info->w + 1,
      XtNheight, iconData->info->h + 1,
      XtNbackgroundpixmap, pix,
      XtNHighlightThickness,1,
      NULL);
    XtAddEventHandler(btn, EnterWindowMask, False,
      (XtEventHandler)statusProc,
      -(XtPointer)iconData->msg);
    XtAddEventHandler(btn, LeaveWindowMask, False,
      (XtEventHandler)statusProc, (XtPointer)NULL);
 
    XtAddCallback(btn, XtNcallback, callback,
      -(XtPointer)iconData->func);
  }
}
/*
 * go to the next element
 */
```

## 274 第四部分 布局

### 列表 13.4 续

```c
101: iconData++;
102:   }
103: }
104:
/*
 * 创建一个按钮面板，用于控制应用程序
 */
void create_buttons( Widget parent)
{
  Widget btnPanel, exitB;
 
/*
 * 为绘图图标创建一个面板
 */
  btnPanel = XtVaCreateWidget( "drawBtnPanel",
    boxWidgetClass, parent,
    XtnTop, XawChainTop,
    XtnRight, XawChainRight,
    XtnBottom, XawChainTop,
    XtnLeft, XawChainRight,
    XtnHorizDistance, 0,
    XtnFromHorizon, GxDrawArea,
    XtnSpace, 1,
    XtnVSpace, 1,
    NULL );

  create_icons(btnPanel, gDrawIcons, draw_manager);
  XtManageChild(btnPanel);
/*
 * 为控制图标创建一个面板
 */
  btnPanel = XtVaCreateWidget( "ctrlBtnPanel",
    boxWidgetClass, parent,
    XtnTop, XawChainTop,
    XtnRight, XawChainRight,
    XtnBottom, XawChainTop,
    XtnLeft, XawChainRight,
    XtnFromHorizon, btnPanel,
    XtnHorizDistance, 0,
    XtnSpace, 1,
    XtnVSpace, 1,
    NULL );

  create_icons(btnPanel, gCntIcons, ctrl_manager);
  XtManageChild(btnPanel);
  exitB = XtVaCreateManagedWidget( "
    commandWidgetClass, parent,
```

## 应用结构第 13 章 275
