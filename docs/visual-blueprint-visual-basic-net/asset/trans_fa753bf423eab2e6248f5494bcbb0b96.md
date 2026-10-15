

## 选择数值数据

你可以使用 TrackBar 控件让用户选择数值或其他有序数据。TrackBar 控件提供了一个滑块，可以水平（从左到右）或垂直（从上到下）显示。

TrackBar 为 Orientation 属性提供了两种设置。Horizontal 使控件左右滑动。Vertical 使控件上下滑动。将其放在窗体上后，控件在水平模式下不会改变高度，在垂直模式下不会改变宽度。

Minimum 属性确定用户将滑块移动到左侧或顶部位置时可以选择的最小值。Maximum 属性确定用户在滑块条的右侧或底部位置可以选择的最大值。你可以在设计时或在代码中设置 Value 属性来定位滑块。当用户移动滑块时，Value 属性也会更新。

在控件显示中，滑块条会指向一组刻度标记。刻度是控件上表示滑块值的小短划线。TickFrequency 属性决定控件显示的刻度数。例如，如果 TrackBar 的范围是 0 到 10，并且 TickFrequency = 1，则 TrackBar 包含 11 个刻度，每个值对应一个刻度。如果 TickFrequency 为 2，则刻度会每隔一个值显示一个。TickStyle 属性允许你将刻度放置在 BottomRight（水平条的底部，垂直条的右侧）、TopLeft、Both 或 None。

当用户使用鼠标或键盘移动滑块时，会触发 Scroll 事件。事件触发前，Value 属性会更新为滑块的新位置，因此你可以显示数值或根据滑块在事件中的位置做出相应的更改。

![](img/d6f772854306e15fb6df39b861a7b541_79_0.png)

1. 在 Windows 应用程序项目中，添加一个控件来响应滑块的值。示例添加了一个 Label 控件。
2. 从工具箱中将 TrackBar 控件拖放到窗体上。
3. 在“属性”窗口中，双击 Orientation 属性以在两个值之间切换。
4. 为 Minimum 属性输入一个整数值。
5. 为 Maximum 属性输入一个整数值。
6. 编辑其他任何属性。注意：若要编辑属性，请参阅第 2 章。
7. 双击控件以添加 Scroll 事件的代码。

   此时将显示代码编辑器。

8. 若要在窗体上检索 TrackBar 值，请键入控件名称后跟 .Value。
9. 按 F5 运行程序。

用户可以根据需要移动滑块。

### 补充

你可以使用 TrackBar 控件可用的事件，使鼠标滚动成为滚动浏览控件值的有效方法。如果用户使用鼠标滚轮移动滑块，控件不会引发 Scroll 事件，而是引发 MouseWheel 事件。你可以从 MouseWheel 事件调用 Scroll 事件来执行相同的功能。

你可以操作属性，使用户能够轻松地在值范围内移动。SmallChange 属性指定滑块移动的最小增量。你可以使用它来决定当用户拖动滑块时，滑块会移动到哪些值。例如，值为 2 时，用户移动 TrackBar 时只能每隔一个数字选择一个值。LargeChange 属性决定当用户点击滑块条，或使用 Page Up 和 Page Down 键在滑块两侧移动时，滑块移动的幅度。

示例：

```vb
Private Sub TrackBar1_Scroll(ByVal sender As _
    System.Object, ByVal e As _
    System.EventArgs) Handles TrackBar1.Scroll
    Label1.Text = TrackBar1.Value.ToString()
End Sub
Private Sub TrackBar1_MouseWheel(ByVal sender As _
    Object, ByVal e As _
    System.Windows.Forms.MouseEventArgs) _
    Handles TrackBar1.MouseWheel
    TrackBar1_Scroll(sender, e)
End Sub
```

![](img/d6f772854306e15fb6df39b861a7b541_80_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_80_1.png)

