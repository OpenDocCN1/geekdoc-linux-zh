

```cpp
inline int GetY2() { return _y2; }
};
class TCanvasPane : public vCanvasPane {
private:
    bool mouseDown;      // True while mouse button down
    int x1, y1, x2, y2;  // Line coordinates
    vector<TLine> lines; // Array of TLine objects
public:
    TCanvasPane();       // Constructor
    ~TCanvasPane();      // Destructor
    // Override some inherited functions
    virtual void MouseDown(int x, int y, int button);
    virtual void MouseUp(int x, int y, int button);
    virtual void MouseMove(int x, int y, int button);
    virtual void Redraw(int x, int y, int w, int h);
};
```

为了存储每条线的坐标值——当窗口被覆盖后重新显示或被调整大小时需要重绘画布——该模块声明了一个 TLine 类。如何为你的应用程序存储图形信息由你决定，但我在这里使用了一个类，因为更复杂的图形程序可能会基于相关类的层次结构来定义所有形状。

TCanvasPane 类派生自 V 的 vCanvasPane，首先定义了一些私有数据成员，用于维护图形输出。变量 mouseDown 在用户按住鼠标按钮时为 true，而整数变量表示正在绘制的线。vector<TLine> 类实例化了标准模板库的 vector 模板，以创建一个用于跟踪线坐标的容器。

TCanvasPane 的 public 部分中的声明包括大多数类中常用的构造函数和析构函数，以及另外四个函数。其中前三个显然与鼠标按钮点击和移动有关。第四个 Redraw() 用于绘制画布的输出。

这些函数原型覆盖了从 vCanvasPane 类继承的同名函数。每个函数都与特定类型的事件相关联。例如，按下按钮事件会使 V 调用画布的 MouseDown() 虚函数。这是一个很好的例子，说明如何使用虚 C++ 函数轻松更改对象的行为。在本例中，我们希望在用户点击并拖动鼠标时绘制线条，因此我们只需覆盖窗口画布的虚鼠标函数，让 V 来决定如何以及何时调用这些函数。

Redraw() 函数是所有 V 应用程序中最关键的函数之一。它等同于 Xlib 的 Expose 事件，要求窗口重新创建其内容。一般来说，要在窗口中创建图形输出，只需将绘图命令添加到画布的 Redraw() 函数中。下一个模块，清单 30.8，canvas.cpp，展示了 vSketch 中是如何实现的。

## LISTING 30.8 VSKETCH/CANVAS.CPP

```cpp
#include "canvas.h"

// Constructor
TCanvasPane::TCanvasPane():
    vCanvasPane(),  // Call ancestor constructor
    lines()         // Construct lines vector (grows as needed)
{
    mouseDown = false;
    x1 = y1 = x2 = y2 = 0;
}

// Destructor
TCanvasPane::~TCanvasPane()
{
    // Nothing to do!
}

// Respond to mouse button click event
// Prepares for drawing the next line
void TCanvasPane::MouseDown(int x, int y, int button)
{
    mouseDown = true;   // Set mouse down flag
    x1 = x;             // Remember starting location
    y1 = y;
    x2 = x1;            // Set end point == beginning
    y2 = y1;            // as a "do nothing" flag
}

// Respond to mouse button release event
// Save current line in the lines vector
void TCanvasPane::MouseUp(int x, int y, int button)
{
    mouseDown = false;  // Reset mouse down flag
    if (x1 != x2 || y1 != y2) {
        DrawRubberLine(x1, y1, x2, y2);  // Erase old line
        x2 = x;          // Save line end point
        y2 = y;
        DrawLine(x1, y1, x2, y2);  // Draw fixed line
        lines.push_back(TLine(x1, y1, x2, y2));  // Save line
    }
}

// Respond to mouse movement event
// Draws a "rubber" line (i.e. an erasable line)
void TCanvasPane::MouseMove(int x, int y, int button)
{
    if (mouseDown) {
        if (x1 != x2 || y1 != y2) {
            DrawRubberLine(x1, y1, x2, y2);  // Erase old line
            x2 = x;   // Save line end point so far
            y2 = y;
            DrawRubberLine(x1, y1, x2, y2);  // Draw new line
        }
    }
}
```

