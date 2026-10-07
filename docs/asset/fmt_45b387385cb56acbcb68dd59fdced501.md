
```c
/* 处理按钮按下 */
SDL_MOUSEBUTTONDOWN:
case
  printf("Mouse button %d pressed at (%d, %d)\n",
      button->button, button->x, button->y);
  break;
```

```c
/* 处理按钮释放 */
SDL_MOUSEBUTTONUP:
  printf("Mouse button %d released at (%d, %d)\n",
      button->button, button->x, button->y);
  break;
```

```c
/* 这不应该被到达 */
default:
  break;
}
```

## 摇杆事件

如果你认为那两个键盘结构和鼠标结构已经很费力了，那么你一定会非常喜欢处理摇杆事件。总共有四种摇杆事件结构——但别担心，它们都非常相似。当你理解了它们的相似之处后，理解它们的区别就轻而易举。然而，在探索摇杆事件结构之前，我们必须理解让摇杆与键盘和鼠标不同的一个点。摇杆不被视为强制性设备。必须向 `SDL_Init` 传递 `SDL_INIT_JOYSTICK` 标志以启用其摇杆子系统。SDL 假设系统中只连接了一个键盘和一个鼠标，但它理解系统中可能、且通常连接了一个或多个摇杆。因此，你必须指定要使用哪些摇杆；当然，SDL 提供了函数允许你完成这一点。

```c
int SDL_NumJoysticks(void);
```

`SDL_NumJoysticks()` 函数应该是你在处理摇杆时始终采取的第一步。它返回连接到系统的摇杆数量。如果它返回 0，那么就没有必要尝试打开任何摇杆，因为那里什么都没有。

```c
SDL_Joystick *SDL_JoystickOpen(int index);
```

`SDL_JoystickOpen()` 函数打开一个摇杆并返回一个指向结构的指针，该结构存储了摇杆的信息。你应该保存返回的结构指针，因为在关闭摇杆时会需要它。你想打开的摇杆通过 `Index` 参数指定（0 表示第一个摇杆，1 表示第二个，以此类推）。`Index` 是一个非常重要的值，因为它被事件结构用于标识是哪个摇杆生成的事件。当你完成摇杆的使用后，良好的做法是通过传递 `SDL_JoystickClose()` 返回的 `SDL_Joystick` 结构来关闭它。

如果你对摇杆一无所知，即使打开了摇杆也没用，对吧？SDL 提供了几个函数来获取摇杆名称，以及获取可用轴（axes）、按钮、帽（hats）和球（balls）的数量。这些函数如下：

```c
const char *SDL_JoystickName(int index)
```

```c
int SDL_JoystickNumAxes(SDL_Joystick *joystick)
```

```c
int SDL_JoystickNumButtons(SDL_Joystick *joystick)
```

```c
int SDL_JoystickNumHats(SDL_Joystick *joystick)
```

```c
int SDL_JoystickNumBalls(SDL_Joystick_)
```

这五个函数的功能简单，SDL 文档中有清晰的解释。你将在后面的示例中使用这些函数。

默认情况下，SDL 事件队列不会从已打开的摇杆收集事件，你必须通过调用 `SDL_JoystickEventState(SDL_ENABLE)` 显式地指示队列这样做。如果没有此调用，你只能轮询摇杆输入。

四个与摇杆相关的事件结构都具有相似的布局，如这些结构原型所示：

```c
typedef struct {
  Uint8 type;
  Uint8 which;
  Uint8 axis;
  Uint16 value;
} SDL_JoyAxisEvent;
```

```c
typedef struct {
  Uint8 type;
  Uint8 which;
  Uint8 button;
  Uint8 state;
} SDL_JoyButtonEvent;
```

```c
typedef struct {
  Uint8 type;
  Uint8 which;
  Uint8 hat;
  Uint8 value;
} SDL_JoyHatEvent;
```

```c
typedef struct {
  Uint8 type;
  Uint8 which;
  Uint8 ball;
  S16 xrel, yrel;
} SDL_JoyBallEvent;
```

所有四个结构中的前两个字段具有相同的含义。`type` 字段的含义与其他其他事件结构中的 `type` 字段相同；`which` 指的是哪个摇杆事件。它的值与传递给 `SDL_JoyAxisOpen()` 的 `index` 参数相同。每个事件结构中的第三字段指示该事件指的是哪个轴、按钮、帽或球。对于第三个字段，值 0 表示第一个轴、按钮、帽或球；第二个是第二个，以此类推。注意该字段在每个结构中的命名不同：在 `SDL_JoyAxisEvent` 中，字段名为 `axis`；在 `SDL_JoyBallEvent` 中，字段名为 `ball`；以此类推。

每个结构变量包含的输入数据类型。`SDL_JoyAxisEvent` 在 `value` 字段中包含新位置，该字段在本章开头解释为带符号 16 位整数。帽只有九个位置，`SDL_JoyHatEvent` 的 `value` 字段包含以下之一：

- `SDL_HAT_CENTERED`

- `SDL_HAT_UP`

- `SDL_HAT_RIGHTUP`

- `SDL_HAT_RIGHT`

- `SDL_HAT_RIGHTDOWN`

- `SDL_HAT_DOWN`

- `SDL_HAT_LEFTDOWN`

- `SDL_HAT_LEFT`

- `SDL_HAT_LEFTUP`

与其他摇杆控件不同，球没有位置；它们只报告相对于上一次读取的移动。这些数据存储在 `SDL_BallEvent` 结构的 `xrel` 和 `yrel` 字段中。

## 使用 SDL 进行输入

摇杆并不复杂，但在编写代码处理它们时你必须小心。你必须确保你的代码能够通过正确处理 `which` 和 `control` 字段来处理许多不同类型的配置。接下来的示例演示了解释摇杆事件的基础。

```c
void Handle(SDL_Event *event){
  /* 指向结构的有用指针 */
  SDL_JoyAxisEvent *axis = event->axis;
  SDL_JoyButtonEvent *button = event->button;
  SDL_BallEvent *ball = event->ball;
  SDL_JoyHatEvent *hat = event->hat;

  /* 根据类型进行分支 */
  switch(event->type) {
    /* 轴运动 */
    case SDL_JOYAXMOTION:
      printf("Joystick %d, Axis %d %d\n", axis->which, axis->axis, axis->value);
      break;

    /* 按钮按下 */
    case SDL_JOYBUTTONUP:
      printf("Joystick %d, Button %d released\n", button->which, button->button);
      break;

    /* 按钮释放 */
    case SDL_JOYBUTTONDOWN:
      printf("Joystick %d, Button %d pressed\n", button->which, button->button);
      break;

    /* 球体运动 */
    case SDL_JOYBALLMOTION:
      printf("Joystick %d, Ball %d %d, %d\n", ball->which, ball->ball, ball->xrel, ball->yrel);
      break;

    /* 帽运动 */
    case SDL_JOYHATMOTION:
      printf("Joystick %d, Hat %d %d\n", hat->which, hat->hat, hat->value);
      /* 根据帽的位置分支 */
      switch(hat->value) {
        case SDL_HAT_CENTERED:
          printf("Center");
          break;
        case SDL_HAT_UP:
          printf("Up");
          break;
        case SDL_HAT_RIGHTUP:
          printf("Up-right");
          break;
        case SDL_HAT_RIGHT:
          printf("Right");
          break;
        case SDL_HAT_RIGHTDOWN:
          printf("Down-right");
          break;
        case SDL_HAT_DOWN:
          printf("Down");
          break;
        case SDL_HAT_LEFTDOWN:
          printf("Down-left");
          break;
        case SDL_HAT_LEFT:
          printf("Left");
          break;
        case SDL_HAT_LEFTUP:
          printf("Up-left");
          break;
      }
      break;

    /* 这不应该被到达 */
    default:
      break;
  }
}
```

*(注：由于原文文本中 `Handle` 函数的 示例代码逻辑存在多处混乱和未完成的语法错误（如 `axis->which` 与 `ball` 变量混用），翻译时已根据代码意图进行了逻辑微调以保持可读性，但保留了原始结构。)*

## 使用 SDL 进行输入

摇杆并不复杂，但在编写代码处理它们时你必须小心。你必须确保通过正确处理 `which` 和 `control` 字段，你的代码能够处理许多不同类型的配置。接下来的示例演示了解释摇杆事件的基础。

```c
void Handle(SDL_Event *event){
  /* 指向结构的有用指针 */
  SDL_JoyAxisEvent *axis = event->axis;
  SDL_JoyButtonEvent *button = event->button;
  SDL_BallEvent *ball = event->ball;
  SDL_JoyHatEvent *hat = event->hat;

  /* 根据类型进行分支 */
  switch(event->type) {
    /* 轴运动 */
    case SDL_JOYAXMOTION:
      printf("Joystick %d, Axis %d %d\n", axis->which, axis->axis, axis->value);
      break;

    /* 按钮按下 */
    case SDL_JOYBUTTONUP:
      printf("Joystick %d, Button %d released\n", button->which, button->button);
      break;

    /* 按钮释放 */
    case SDL_JOYBUTTONDOWN:
      printf("Joystick %d, Button %d pressed\n", button->which, button->button);
      break;

    /* 球体运动 */
    case SDL_JOYBALLMOTION:
      printf("Joystick %d, Ball %d %d, %d\n", ball->which, ball->ball, ball->xrel, ball->yrel);
      break;

    /* 帽运动 */
    case SDL_JOYHATMOTION:
      printf("Joystick %d, Hat %d %d\n", hat->which, hat->hat, hat->value);
      /* 根据帽的位置分支 */
      switch(hat->value) {
        case SDL_HAT_CENTERED:
          printf("Center");
          break;
        case SDL_HAT_UP:
          printf("Up");
          break;
        case SDL_HAT_RIGHTUP:
          printf("Up-right");
          break;
        case SDL_HAT_RIGHT:
          printf("Right");
          break;
        case SDL_HAT_RIGHTDOWN:
          printf("Down-right");
          break;
        case SDL_HAT_DOWN:
          printf("Down");
          break;
        case SDL_HAT_LEFTDOWN:
          printf("Down-left");
          break;
        case SDL_HAT_LEFT:
          printf("Left");
          break;
        case SDL_HAT_LEFTUP:
          printf("Up-left");
          break;
      }
      break;

    /* 这不应该被到达 */
    default:
      break;
  }
}
```

## 鼠标轮询

与键盘轮询类似，你也可以使用以下函数以非常的方法轮询鼠标。

`Uint8 SDL_GetMouseState(int *x, int *y);`

`Uint8 SDL_GetRelativeMouseState(int *x, int *y);`

获取当前鼠标位置和按钮状态是一项简单的任务。`SDL_GetMouseState()` 函数将当前鼠标位置拷贝到传入的 x 和 y 指针中，并返回与 `SDL_MouseMotionEvent` 结构中存储的按钮数据格式相同的按钮状态。`SDL_GetRelativeMouseState()` 函数返回相同的按钮数据；但其位置是相对于上一次鼠标位置的，而不是屏幕原点。

## 配置控制系统

一个可以由用户完全配置的控制系统提供了完全的自由。然而，这样的系统也可能在用户开始游戏之前提供过多的选择和选项，让他们感到无所措。请注意，你应该始终允许用户对若干功能进行配置。例如，用户应该能够按照喜好重新映射键盘键和按钮。鼠标和摇杆的灵敏度应该是可调节的。值得注意的是，某些摇杆的按钮在硬件看来实际上可能是轴，因此你应该小心不要将轴仅限制为按钮，例如模糊的控制或视角缩放。

> 不要根据你自己的个人偏好做出假设。记住，你不会是唯一玩你游戏的人。如果可能，让朋友和同事测试你的控制方法和配置选项。

实现这一点的简单且有效的方法是使用一个包含按键的结构体以及一个在激活相应输入时调用的函数指针。下面的示例代码演示了这一点。

```c
#define KEY_UP 0
#define KEY_DOWN 1
#define KEY_LEFT 3
#define KEY_RIGHT 4
#define KEY_FIRE 5
```

```c
typedef struct {
    unsigned int key;
    void (*func_ptr)(void);
} KeyMap;
// 定义默认键盘映射
KeyMap DefaultMap[] = {
    (SDL_KEYUP, UpButton),
    (SDL_KEYDOWN, DownButton),
    (SDL_KEYRIGHT, RightButton),
    (SDL_KEYLEFT, LeftButton),
    (SDL_SPACE, FireButton),
    (0, NULL)
};
```

当需要更改输入映射时，只需更改 `KeyMap` 函数中对应事件的 `key` 成员的关联按键即可。当你检查输入时，参考映射结构并调用相应的函数。

# 第 6 章

## LINUX 游戏的 3D 图形

# LINUX 游戏编程

多年来，3D 在游戏中越来越受到重视，诸如《毁灭战士争霸 III》和《半条命》等作品向开发者展示了他们应该做什么。为了方便我们的工作，几家公司开发了 3D API 来处理 3D 编程中更复杂的方面。

## 一段历史！MESA 和 OPENGL

目前，只有两种 3D 图形接口在计算机游戏领域常用：Direct3D 和 OpenGL。Direct3D 仅在 Microsoft Windows 下可用，但 OpenGL 实现在几乎每种能够运行 3D 图形的计算机上——包括各种机器。因此，当快速的 3D 图形硬件来到 PC 时，Linux 需要某些 OpenGL 实现是不可避免的。
