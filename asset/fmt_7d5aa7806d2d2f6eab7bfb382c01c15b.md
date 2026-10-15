
```
int GetDeviceCaps(
  HDC hdc          // DC 的句柄
  int nIndex      // 能力索引
);

void myFunction(HWND hThisWindow) 
{
  HDC hdc;

  hdc = GetDeviceCaps(hdc, HORZRES);
  widthOfScreenPixels   = GetDeviceCaps(hdc, HORZRES);
  numberOfPlanes       = GetDeviceCaps(hdc, PLANES);
  numberOfColors        = GetDeviceCaps(hdc, NUMCOLORS);
  numberOfFonts        = GetDeviceCaps(hdc, NUMFONTS);

}
```

## 绘制二维线条和形状

绘图表面的设备上下文（device context）包含了某些会直接影响线条、曲线和矩形绘制方式的属性。这些属性包括当前的画刷、画笔以及当前位置。

任何给定 DC 的默认当前位置是逻辑（世界）二维空间中的 `(0,0)`。可以通过调用 `MoveToEx()` 来更改当前位置的值，如下代码示例所示。`MoveToEx()` 函数将当前位置更新为指定点，并可选地返回之前的位置。此函数影响后续所有的绘图操作。

```
BOOL MoveToEx(
// 设备上下文句柄
    HDC hdc,                // 新当前位置的 x 坐标
    int X,                  // 新当前位置的 y 坐标
    LPPOINT lPoint          // 旧当前位置
);
```

`POINT` 结构定义了点的 x 和 y 坐标，如下代码示例所示：

```
typedef struct tagPOINT {
    LONG x;
    LONG y;
} POINT, *PPOINT;
```

## 绘制线条

Win32 GDI API 了两组和曲线绘制函数。这两组函数通过函数名结尾的 "To" 字母来区分。以 "To" 结尾的函数使用并设置当前位置。不以 "To" 结尾的函数则保持当前位置不变。

`LineTo` 函数从当前位置绘制到指定点（但不包含该点），如下代码示例所示：

```
BOOL LineTo(
// 设备上下文句柄
    HDC hdc,                // 终点的 x 坐标
    int nXEnd,              // 终点的 y 坐标,
);
```

`PolylineTo` 函数绘制一条或多条直线，这些直线使用并更新当前位置。函数使用当前画笔从当前位置绘制到 `lppt` 参数指定的第一个点。对于后续每条线，函数都从上一条线的终点绘制到 `lppt` 确定的下一个点，如下代码示例所示：

```
BOOL PolylineTo(
// 设备上下文句柄
    HDC hdc, 
    CONST POINT *lppt, // 点数组
    DWORD cCount             // 数组中的点数
);
```

`Polyline` 函数通过连接指定数组中的点来绘制一系列线段，如下代码示例所示。线条使用当前画笔从第一个点通过后续点绘制。与 `LineTo()` 或 `PolylineTo()` 函数不同，`Polyline()` 函数不会更新当前位置。

```
BOOL Polyline(
    HDC             hdc,      // 设备上下文句柄
    CONST POINT *lppt,  // 终点数组
    int             cPoints  // 数组中的点数
);
```

以下 X Windows 示例显示了 `XDrawLine()` 的用法：

```
int main (int argc, char **argv)
{
    XtToolkitInitialize();

    myApplication = CreateAppContext();

    myDisplay = XtOpenDisplay(myApplication,
                               NULL,
                               NULL,
                               "XBlaat",
                               NULL,
                               &argc,
                               argv);

    myWindow = RootWindowOfScreen(DefaultScreenOfDisplay (mydplay));
    //+
    // 现在我们需要一个用于绘图的表面
    //-
    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myGC = XCreateGC (myDisplay,mySurface, GCForeground, 
    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myGC = XCreateGC (myDisplay,mySurface, GCForeground, 
    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myGC = XCreateGC (myDisplay,mySurface, GCForeground, 
    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myGC = XCreateGC (myDisplay,mySurface, GCForeground, 
    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myGC = XCreateGC (myDisplay,mySurface, GCForeground, 
    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myGC = XCreateGC (myDisplay,mySurface, GCForeground, 
    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));

    myGC = XCreateGC (myDisplay,mySurface, GCForeground, 
    myMap = XCreatePixmap (myDisplay,myWindow,64,64, 1);

    values.foreground = =
        BlackPixel(myDisplay,DefaultScreen (myDisplay));
```

以下 Win32 示例显示了 `MoveToEx()` 和 `LineTo()` 的用法：

```cpp

void lineExample( HDC )

{

    HPEN oldPen;

    //+

 使用 使用画笔

    //- 

    oldPen = SelectObject(hDC, myPen);

    //+

// 设置当前位置。

    // 如果已知当前位置在 (0,0)。

    //- 

    MoveToEx(hDC, 0, NULL );

    //+

// 现在当前位置在 (63,63)

    //- 

    LineTo( hDC, 63, 0 );

    //,

}

```

## 绘制矩形

在 Win32 中，Rectangle形状是一个填充形状。填充形状是当前画笔可以勾勒、当前画刷可以填充的几何图形。填充形状有五：

- 圆圆 (Ellipse)
- 弧 (Chord)
- 扇形 (Pie)
- 多边形 (Polygon)
- 矩形 (Rectangle)

在 Windows 中，Rectangle形状与 Win32 等效形式大不同。在两者之间移植时，需要理解这种差异。X Windows 版本使用左上角点以及宽度高度。Win32 版本使用左上角和右下角点。对于 `XDrawRectangle()` 和 Win32 `Rectangle()` 函数也是如此。

X Windows 结构如下：

```
typedef struct {

  short x,y;

  unsigned short width,height;

} XRectangle;
```

其 Win32 等效形式如下：

```cpp

typedef struct _RECT {

  LONG left;

  LONG top;

  LONG right;

  LONG bottom;

} RECT;

```

`Rectangle()` 函数绘制一个矩形。该矩形使用当前画笔勾勒，使用当前画刷填充。由于它不填充矩形，该函数与 `XDrawRectangle()` 函数不同。

```
BOOL Rectangle(

  HDC hdc, // DC 的句柄

  int nLeftRect, // 矩形左上角的 x 坐标

  int nTopRect, // 矩形左上角的 y 坐标

  int nRightRect, // 矩形右下角的 x 坐标，

  int nBottomRect // 矩形右下角的 y 坐标

);
```

填充矩形的函数有：

- X Windows: `XFillRectangle()`
- Win32: `Rectangle()`
- Win32: `FillRect()`

仅绘制轮廓的矩形函数有：

- X Windows: `XDrawRectangle()`
- Win32: `FrameRect()`

注意：Win32 函数 `Rectangle()` 和 `FillRect()` 接受的参数不同。更多信息请参阅 Visual Studio 帮助文档或 MSDN 网站 `http://msdn.microsoft.com/`。

以下 X Windows 示例演示了矩形函数：

```
void drawSomeRectangles()

{

    //+

    // 填充矩形，然后在周围绘制黑色边框

    //- 

    XFillRectangle(myDisplay, mySurface, myWhiteGC, 0, 0, 31, 31);

    XDrawRectangle(myDisplay, mySurface, myBlackGC, 0, 0, 31, 31);

    //+

    // 绘制一个十像素见的空矩形

    //- 

    XDrawRectangle(mDisplay, mySurface, myBlackGC, 0, 0, 10, 10);

}
```

以下 Win32 示例演示了矩形函数：

```c

void drawSomeRectangles( )

{

    RECT myRectangle;

    //+

    // 填充矩形，然后在周围绘制黑色边框

    // 假设当前 DC 中的画笔是黑色的，

    // 当前画刷不是

    //- 

    Rectangle( hDC, 0, 0, 31, 31 );

    //+

    // 绘制一个十像素见的空矩形

    // FrameRect() 函数使用指定的画刷而非当前

    // 画笔，在指定的矩形周围绘制边框。

    //

    // 边框的宽度和高度始终为一个逻辑单位。

    //- 

    myRectangle.Top = 0;

    myRectangle.Left = 0;

    myRectangle.Bottom = 10;

    myRectangle.Right = 10;

    FrameRect( hDC, &myRectangle, myBlackBrush );

}
```

## 超时与定时器

需要定时器来确定并处理用户输入中的延迟。后续章节将讨论 X Windows 超时和 Win32 定时之间的功能及其区别。

## X Windows 超时

X Windows 客户端可以使用 `XtAppDataTimeOut()` 和 `XtRemoveTimeOut()` 函数配合回调函数，根据以毫秒为单位指定的间隔进行处理。以下代码显示了此类示例：

```c

//+

// 每秒执行一次任务

//-

void myTimerProc( Widget w,

                   XEvent *event,

                   String *pars,

                   Cardinal *npars)

{

    ...

}
```

```c

//+

// 启动 1 秒定时器

//-

void startTimer( XtIntervalId *timer )

{

    (*timer) = XtAppDataTimeOut(gContext, 1000, myTimerProc, NULL);

}
```

```c

//+

// 停止定时器

//-

void stopTimer( XtIntervalId * timer )

{

    if(*timer) {

        XtRemoveTimeOut(*timer);

        (*timer) = NULL;

    }

}
```

## Win32 定时器

Windows 定时器可以用两种场景：首先，类似于 X Windows 方法，可以指定一个回调函数在每个定时器间隔执行。其次，可以使用消息（`WM_TIMER`）来处理定时器间隔。

以下示例了使用 Win32 定时器的回调版本：

```c

//+/

// 每 1 秒执行一次任务

//-

void CALLBACK myTimerProc( HWND w,

	UINT timerMessage,

	UINT PTR timerID,

	DWORD systemTime )

{

    nnn
//+

// 启动 1 秒定时器

//-

void startTimer( UINT_PTR *timer, UINT_PTR timerID )

{

	(*timer) = SetTimer( hParent, timerID, 1000, myTimerProc);

}

//+

// 停止定时器

//-

void stopTimer( UINT_PTR *timer )
{
