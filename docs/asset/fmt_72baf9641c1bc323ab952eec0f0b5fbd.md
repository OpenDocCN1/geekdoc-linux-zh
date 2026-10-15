
# 第 12 章. 输入设备函数

`handler` 指定程序提供的错误处理器。

`handler` 设置致命的 I/O 错误处理器。如果发生任何类型的系统调用错误（例如与服务器的连接丢失），`Lib` 会调用程序提供的错误处理器。这被认为是一个致命条件，调用的程序不应返回。如果 I/O 错误处理器返回了，客户端进程将退出。

注意，会返回之前的错误处理器。

## 指针捕取

你可以使用 `XLib` 输入设备函数来：

- 捕取指针和指针上的单个按钮
- 捕取键盘和键盘上的单个按键
- 恢复事件处理
- 移动指针
- 设置输入焦点
- 操作键盘和指针设置
- 操作键盘编码

`XLib` 提供了你可以使用来控制指针（通常是鼠标）输入的函数。通常情况下，一旦键盘和鼠标事件发生，`X` 服务器就会将它们传递给适当的客户端，该客户端由窗口和输入焦点决定。`X` 服务器对事件传递提供了足够的控制，允许窗口管理器支持鼠标提前触发和各种用户界面样式。许多此类界面依赖于事件的同步传递。指针和键盘事件的传递可以独立控制。

当按钮或键盘按键被捕获时，事件将发送给捕获客户端，而不是本应接收该事件的客户端。如果指针处于异步模式，后续的鼠标和键盘事件将继续处理。如果键盘或指针处于同步模式，则在捕获客户端允许（`XAllowEvents`）之前，将不再处理后续事件。在此期间，键盘或指针被认为冻结。触发捕获的事件可以重放。

注意，设备的逻辑状态（客户端应用程序看到的）在事件处理期间可能会滞后于物理状态。

捕取有两种类型：主动和被动。主动捕获发生在单个客户端显式捕获键盘或指针（`XGrabPointer` 和 `XGrabKeyboard`）。被动捕获发生在客户端捕获窗口中的特定键盘或指针按钮时，并且当键或按钮实际被按下时捕取将激活。被动捕获便于实现可靠的弹出菜单。例如，通过捕获一个请求同步行为的按钮，你可以保证在指针按钮事件发生之前弹出窗口已映射。按下事件（down event）将触发捕获并冻结指针事件的后续处理，直到你有机会映射弹出窗口。然后你可以允许后续的事件处理。释放事件（up event）将相对于弹出窗口被正确处理。

对于许多操作，有接受时间参数的函数。时间戳是一个以毫秒表示的值，通常是自重置以来的时间。时间戳会回绕（49.7 天）。服务器给定其当前时间为 T，解释客户端的时间戳比 T 更晚。一个特殊的时间戳 `CurrentTime`，从不由服务器生成。这被用于表示当前服务器时间。

对于许多函数，你传递指针事件掩码位。有效的掩码位有 `ButtonMask`、`ButtonReleaseMask`、`EnterWindowMask`、`LeaveWindowMask`、`PointerMask`、`PointerHintMask`、`ButtonMask`、`Button2Mask`、`Button3Mask`、`Button4Mask`、`Button5Mask` 和 `KeymapState`。对于其他函数，你传递键掩码位：`ShiftMask`、`LockMask`、`ControlMask`、`Mod1Mask`、`Mod2Mask`、`Mod3Mask`、`Mod4Mask` 和 `Mod5Mask`。

要捕取指针，使用 `XGrabPointer`。

```c
int XGrabPointer(display, grab_window, owner_events, event_mask, pointer_mode, keyboard_mode, confine_to, cursor, time);
```

- `display` 指定与 X 服务器的连接。
- `grab_window` 指定捕获窗口。
- `owner_events` 指定一个布尔值，指示指针事件是按通常报告还是相对于由 `event mask` 选择的获窗口报告。
- `event_mask` 指定哪些指针事件报告给客户端。掩码是有效指针事件掩码位的按位或。
- `pointer_mode` 指定指针事件的后续处理。你可以传递 `GrabModeSync` 或 `GrabModeAsync`。
- `keyboard_mode` 指定键盘事件的后续处理。你可以传递 `GrabModeSync` 或 `GrabModeAsync`。
- `confine_to` 指定限制指针的窗口内或 `None`。
- `cursor` 指定在捕获期间显示的光标或 `None`。
- `time` 指定时间。你可以传递时间戳或 `CurrentTime`。

`XGrabPointer` 积极地控制指针的捕取，如果捕取成功，则返回 `GrabSuccess`。后续的指针事件将仅报告给捕取客户端。`XGrabPointer` 会覆盖该客户端执行的任何活跃的指针捕取。如果 `owner_events` 失败，所有生成的指针事件将相对于捕取窗口进行报告，并且仅在被事件掩码选中时进行报告。如果 `owner_events` 为 `True` 且生成的指针事件通常会报告给此客户端，则按照常报告。否则，该事件将相对于捕取窗口报告，并且仅在被事件掩码选中时进行报告。无论 `owner_events` 的值为何，未报告的事件都将被丢弃。

如果指针模式为 `GrabModeAsync`，指针事件将照常继续。如果指针当前被此客户端冻结，则恢复对该指针的处理。如果指针模式为 `GrabModeSync`，客户端应用程序看到的指针状态看起来像是被冻结了，在捕取客户端调用 `KAllEvents` 或指针释放之前，`X` 服务器将不再产生后续事件。在指针冻结期间，实际的变化不会丢失；它们会被队列在服务器中以便稍后处理。

如果键盘模式为 `GrabModeAsync`，键盘事件不受键盘激活的影响。如果键盘模式为 `GrabModeSync`，客户端应用程序看到的键盘状态看起来像是被冻结了，在捕取客户端调用 `KAllEvents` 或指针释放之前，`X` 服务器将不再产生后续事件。在指针冻结期间，实际的变化不会丢失；它们只是被队列在服务器中以便稍后处理。

如果指定了光标（`cursor`），则无论在哪个窗口中都会显示它。如果指定为 `None`，当指针在捕取窗口或其一个子窗口时，将显示该窗口的普通光标；否则，将显示捕取窗口的光标。

如果指定了限制区域（`confine`），则指针被限制在在该区域内。该窗口不需要与捕取窗口有关系。如果指针初始不在限制区域内，它将在捕取激活之前自动移动（warped）到最近的边缘，并照常生成进入/离开事件。如果限制区域随后被重新配置，指针将根据需要自动移动，以保持其包含在窗口内。

`time` 参数允许你避免在应用程序响应时间过长或存在网络延迟时出现的某些情况。考虑你有两个应用程序，它们在被点击时通常都会捕取指针。如果两个应用程序都使用事件中的时间戳，第二个应用程序可能会更快地唤醒，并在第一个应用程序之前成功捕取指针。然后第一个应用程序将收到一个指示，说明另一个应用程序在其请求被处理之前捕取了指针。

`XGrabPointer` 生成 `EnterNotify` 和 `LeaveNotify` 事件。

如果捕取或限制区域任一不可见，或者窗口完全位于根窗口边界之外，`XGrabPointer` 将失败并返回 `GrabNotViewable`。如果指针被某些其他客户端积极捕取，它将失败并返回 `AlreadyGrabbed`。如果指针被另一个客户端的活跃捕取所冻结，它将失败并返回 `GrabFrozen`。如果指定的等待早于上一次指针捕取时间或晚于当前 `X` 服务器时间，它将失败并返回 `GrabInvalidTime`。否则，上一次指针捕取时间将设置为指定的时间（`CurrentTime` 被替换为 `X` 服务器时间）。

`XGrabPointer` 可以产生 `BadCursor`、`BadValue` 和 `BadWindow` 错误。

要取消捕取指针，请使用 `XUngrabPointer`。

```c
XUngrabPointer(display, time);
```

- `display` 指定到 X 服务器的连接。
- `time` 指定时间。你可以传递时间戳或 `CurrentTime`。

如果客户端已通过 `XGrabPointer`、`XGrabButton` 或普通按键捕获了指针，`XUngrabPointer` 将释放指针和任何队列中的事件。如果指定的时间早于上一次指针捕取时间或晚于当前 `X` 服务器时间，则 `XUngrabPointer` 不释放指针。它会生成 `EnterNotify` 和 `LeaveNotify` 事件。如果用于活跃指针捕取的窗口或窗口的限制区域变得不可见，或者由于重新配置导致限制区域到窗口的窗口位于根窗口边界之外，`X` 服务器将自动执行 `XGrabPointer` 请求。

要更改活跃的指针捕取，请使用 `XChangeActivePointerGrab`。

```c
XChangeActivePointerGrab(display, event_mask, cursor, time);
```
