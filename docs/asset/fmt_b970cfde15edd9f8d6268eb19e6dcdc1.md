
```
1: #include <X11/Xaw/Label.h>
2: /*
3: * create_
4: */
5: void create_status(Widget parent, Widget fvert)
6: {
7: GxStatusBar = XtvaCreateManagedWidget("statusBar",
8: labelWidgetClass, parent,
9: Xtnop, XawChainBottom,
10: XtnLeft, XawChainLeft,
11: XtnBottom, XawChainBottom,
12: XtnRight, XawChainRight,
13: XtnFromVert, fvert,
14: XtnBorderWidth, 0,
15: NULL);
16: setStatus("2D-GX (c)Sarry Knight Knight Software - Ready...");
17: } /*
18: * setStatus
19: */
20: void setStatus(char *message)
21: {
22: XtSetValues(GxStatusBar, Xtnlabel, message, NULL);
23: } /*
24: * statusProc
25: */
26: void statusProc(Widget w, XPointer msg, XEvent *xe, Boolean *flag)
27: {
28: if(msg == NULL)
29: setStatus("\0");
30: else
31: setStatus(msg);
32: }
```

随着图形编辑器应用程序激活更多功能和能力，这些函数的复杂性也随之增加。

`draw_manager` 函数演示了当一个命令被激活时，绘制函数在 `iconData` 数组（`gxDrawIconsArray` 的第二个字段）中指定，并被作为类分配给 `draw_manager` 回调函数。

之前的命令从 `XtPointer` 强制转换为函数指针然后被调用，实现了绘制动作。

`draw_manager` 函数随后将 `draw_func` 指针分配给全局变量 `draw_mgr_func`，该变量对 `drawEventProc` 是可见的。当 `drawEventProc` 处理程序由画布窗口中的 `PointerMotion` 或 `ButtonPress` 事件调用时，它能够调用由 `draw_manager` 回调函数注册的最后一个 `draw_func`。`drawAreaEventProc` 函数的目的是继续处理用户在激活绘制按钮图标时发起的绘制动作。

未来的示例中将添加更多细节，但你应该能够跟踪程序的流程到此为止。

在发布到创建 `GxStatusBar` Label 小部件并定义函数 `statusProc` 之后，请考虑列表 6.12。
