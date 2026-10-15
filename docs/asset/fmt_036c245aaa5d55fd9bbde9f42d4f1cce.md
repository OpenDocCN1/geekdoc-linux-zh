
# 列表 B.4 续

```
34:   },

35:   {&text_icon, (void (*void *))gx_text,

36:     "Draw dynamic text...",

37:   },

38:   /*

39:    * 必须为 NULL

40:   */

41: };

42: 

43:  /*

44:   * 创建应用程序绘制的区域

45:   */

46:  Widget create_canvas(Widget parent)

47:  {

48:   GxDrawArea = Xtcreate("drawingArea",

49:     formWidgetClass, parent,

50:     background,

51:     WhitePixelOf(Screen(parent)),

52:     XtNtop, XawChain,

53:     XtNleft, XawChainLeft,

54:     XtNbottom, XawChainBottom,

55:     XtNright, XawChainRight,

56:     XtNheight, 220,

57:     XtNwidth, 250,

58:     NULL);

59:    XtAddEventHandler(GxDrawArea, PointerMask, False,

60:                               (XtEventHandler)drawAreaProc,

61:                                 (XtPointer)NULL);

62:    XtAddEventHandler(GxDrawArea, ButtonPressMask, False,

63:                               (XtEventHandler)drawAreaProc,

64:                               (XtPointer)NULL);

65:    XtAddEventHandler(GxDrawArea, ButtonReleaseMask, False,

66:                               (XtEventHandler)drawAreaProc,

67:                               (XtPointer)NULL);

68:             return GxDrawArea;

69:     }

70:     /*

71:      * create_status

72:      */

73:     void create_status(Widget parent, Widget fvert) {

74:         GxStatusBar = "statusBar",

75:                             labelWidgetclass, parent,

76:                             XtNtop, XawChainBottom,

77:                             XtNleft, XawChainLeft,

78:                             XtNbottom, XawChainBottom,

79:                             XtNright, XawChainRight,

80:                             XtNVert, fvert,

81:                             XtBorderWidth, 0,

82:                             NULL);

83:         setStatus("2D-GX Galaxy - Ready...");

84:     }

85:     /*

86:      * statusProc

87:      */

88:     void statusProc(Widget w,

89:                     XtPointer msg, XEvent *xe, Boolean flag) 

90:         {

91:             if(msg == NULL)

92:                 setStatus("0");

93:             else

94:                 setStatus(msg);

95:         }
```
