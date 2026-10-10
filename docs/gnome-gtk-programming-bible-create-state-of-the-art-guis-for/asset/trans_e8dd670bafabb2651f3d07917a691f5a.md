

```c
135             g_print("\t\tx=%g\ty=%g\ttitle=%g\tytitle=%g\",\n\t\t\t\t\t\tevent->button.x,event->button.xdn,\n\t\t\t\t\t\tevent->button.xi.lt.event->button.y,\n\t\t\t\t\t\tevent->button.xtilt,event->button.ytilt,\n\t\t\t\t\t\tevent->button.pressure,event->button.button);\n\t\t\tg_print("\t\tx_root=%g\ty_root=%g\ttime=%u\n\n141\t\t\t\tstate=0x%08X\")\n\t\t\t\t\t\tevent->button.x_root,event->button.y_root,\n\t\t\t\t\t\tevent->button.time,event->button.state);\n144\t}\n\n145\tvoid describeEventMotion(gchar \*name,GdkEvent \*event)\n146\t{\n\t\tg_print("%s\t--\tGdkEventMotion\")\n\t\tg_print("\t\tx=%g\ty=%g\txtilt=%g\tytilt=%g\n\n148\t\t\t\t\t\tevent->motion.x,event->motion.y,\n\t\t\t\t\t\tevent->motion.xtilt,event->motion.ytilt,\n\t\t\t\t\t\tevent->motion.pressure,\n\t\t\t\t\t\tevent->motion.is_hint ? \"TRUE\" : \"FALSE\")\n\t\tg_print("\t\tx_root=%g\ty_root=%g\ttime=%u\n\n\t\t\t\tstate=0x%08X\")\n\t\t\t\t\t\tevent->motion.x_root,event->motion.y_root,\n\t\t\t\t\t\tevent->motion.time,event->motion.state);\n\t}\n\n159\tvoid describeEventCrossing(gchar \*name,GdkEvent \*event)\n160\t{\n\t\tgchar \*mode =\n\t\t\tevent->crossing.mode == GDK\_CROSSING\_NORMAL\n\n\t\t\t? \"Normal\" : event->crossing.mode == GDK\_CROSSING\_GRAB\n\n\t\t\t? \"Grab\" : \"Ungrab\";\n\n\t\tg_print("%s\t--\tGdkEventCrossing\")\n\t\tg_print("\t\tx=%g\ty=%g\tx_root=%g\ty_root=%g\tfocus=%s\n\n167\t\t\t\t\t\tevent->crossing.x,event->crossing.y,\n\t\t\t\t\t\tevent->crossing.x\_root,event->crossing.y\_root,\n\t\t\t\t\t\tevent->crossing.focus ? \"TRUE\" : \"FALSE\")\n\t\tg_print("\t\tmode=%s\ttime=%u\tdetail=%d\tstate=0x%08X\n\n\t\t\t\t\t\tmode,event->crossing.time,\n\t\t\t\t\t\tevent->crossing.detail,event->crossing.state);\n\t}\n\n175\tgint eventDelete(GtkWidget \*widget,\n176\t\t\tGdkEvent\*event,gpointer data)\n\n\t\t{\n\n\t\t\treturn(FALSE);\n\t}\n\n179\tgint eventDestroy(GtkWidget \*widget,\n\n\n\t\t\tGdkEvent \*event,gpointer data)\n\n\t\t{\n\n\t\t\tgtk\_main\_quit();\n\n\t\t\treturn(0);\n\t}\n
```

第 36 行到第 41 行创建并初始化了一个 GnomeCanvas，获取根组的地址，并将画布附加到应用程序窗口。

在第 43 行到第 79 行之间，创建并添加了三个项目到根组中。在第 52、64 和 78 行，这三个项目被连接到回调函数 itemEvent()。第二个项目，即矩形（如图 9-3 所示），也在第 66 行通过调用 gtk_signal_connect() 连接到回调函数 rectangleEvent()。一个项目可以连接到任意数量的回调函数，并且每个函数都会针对每个事件被调用。在这个程序中，让一个回调函数响应鼠标点击并移动选定的项是方便的。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_290_0.png)

# 图 9-3：矩形报告所有鼠标活动

第 85 行的回调函数 itemEvent() 会在窗口中每个项目上的每次鼠标点击时被调用。第 88 行对 gnome_canvas_item_raise_to_top() 的调用将该项目置于画布窗口中所有其他项目的前面。

回调函数 rectangleEvent() 仅在矩形中心发生某种事件时才会被调用。该函数不执行任何与显示项目相关的操作。相反，它列出事件中包含的信息。存在不同种类的事件，每种事件都有不同的数据布局，但它们都作为 GdkEvent 到达——这是所有事件类型的联合体。所有事件结构体的第一个数据字段都是一个 type 字段，可以通过检查该字段来确定数据的实际格式。从第 104 行开始，有一个 switch/case 语句，它检测事件类型并调用一个函数来列出该类型的数据。事件类型的数量比事件格式的数量要多。（例如，无论鼠标点击是单击、双击还是多次点击，它们都共享相同的数据布局。）

有一个回调函数，用于显示与七种鼠标事件类型中的每一种事件所附带的**数据**

```text
GDK_ENTER_NOTIFY --  GdkEventCrossing
    x=345 y=120 x_root=445 y_root=248 focus=FALSE
    mode=Normal time=4027445079 detail=0 state=0x00000000
    GdkEvent #10 (from server, with no data)
GDK_MOTION_NOTIFY --  GdkEventMotion
    x=345 y=120 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=445 y_root=248 time=4027449171 state=0x00000000
    GdkEvent #3 (from server, with no data)
GDK_MOTION_NOTIFY --  GdkEventMotion
    x=345 y=121 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=445 y_root=249 time=4027449192 state=0x00000000
    GdkEvent #3 (from server, with no data)
    ...
GDK_MOTION_NOTIFY --  GdkEventMotion
    x=345 y=135 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=445 y_root=263 time=4027449457 state=0x00000000
    GdkEvent #3 (from server, with no data)
GDK_BUTTON_PRESS --  GdkEventButton
    x=345 y=135 xtilt=0 ytilt=0 pressure=0.5 button=1
    x_root=445 y_root=263 time=4027449967 state=0x00000000
    GdkEvent #4 (from server, with no data)
GDK_MOTION_NOTIFY --  GdkEventMotion
    x=346 y=135 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=446 y_root=263 time=4027445007 state=0x00000100
    GdkEvent #3 (from server, with no data)
GDK_MOTION_NOTIFY --  GdkEventMotion
    x=346 y=136 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=446 y_root=264 time=4027445038 state=0x00000100
    GdkEvent #3 (from server, with no data)
    ...
GDK_MOTION_NOTIFY --  GdkEventMotion
    x=363 y=149 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=463 y_root=277 time=4027451089 state=0x00000100
    GdkEvent #3 (from server, with no data)
GDK_MOTION_NOTIFY --  GdkEventMotion
    x=364 y=149 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=464 y_root=277 time=4027451282 state=0x00000100
    GdkEvent #3 (from server, with no data)
GDK_BUTTON_RELEASE -- GdkEventButton

    x=364 y=149 xtilt=0 ytilt=0 pressure=0.5 button=1
    x_root=464 y_root=277 time=4027451619 state=0x000000100
    GdkEvent #7 (from server, with no data)
GDK_MOTION_NOTIFY -- GdkEventMotion

    x=364 y=150 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=464 y_root=278 time=4027451925 state=0x00000000
    GdkEvent #3 (from server, with no data)
GDK_MOTION_NOTIFY -- GdkEventMotion

    x=365 y=150 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=465 y_root=278 time=4027452159 state=0x00000000
    GdkEvent #3 (from server, with no data)
GDK_MOTION_NOTIFY -- GdkEventMotion

    x=396 y=152 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=496 y_root=280 time=4027452333 state=0x00000000
    GdkEvent #3 (from server, with no data)
GDK_MOTION_NOTIFY -- GdkEventMotion

    x=398 y=151 xtilt=0 ytilt=0 pressure=0.5 is_hint=FALSE
    x_root=498 y_root=279 time=4027452343 state=0x00000000
    GdkEvent #3 (from server, with no data)
GDK_LEAVE_NOTIFY -- GdkEventCrossing
    x=401 y=151 x_root=501 y_root=278 focus=FALSE
    mode=Normal time=0 detail=0 state=0x00000000
    GdkEvent #11 (from server, with no data)
```

## 移动画布项目

你可以通过指定项目在 $x$ 和 $y$ 方向上需要移动的距离，将 GnomeCanvas 窗口中的项目从一个位置移动到另一个位置。下面的程序基本上与前面的示例相同，只是增加了一个回调函数，用于检测鼠标移动时是否有按键被按下，如果有，则将项目移动到新位置。

```c
1    /** canvasdrag.c */
2    #include <gnome.h>
3
4    gint eventDelete(GtkWidget *widget,
5                    GdkEvent *event,gpointer data);
6    gint eventDestroy(GtkWidget *widget,
7                    GdkEvent *event,gpointer data);
8    static gint dragEvent(GnomeCanvasItem *item,
9                      GdkEvent *event,gpointer data);
10
```

