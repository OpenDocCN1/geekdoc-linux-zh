
```pascal
procedure TFrmNewEmployee.1stbxManagerMouseDown(Sender:TObject;
Button: TButton; Shift: TShiftState; X, Y: Integer);
begin
  if(Sender as TListbox).(Button = mbLeft) then
    (Sender as TListbox).BeginDrag(false)
end;
```

要执行拖动操作，请使用`BeginDrag`方法。`BeginDrag`声明在`TControl`中并接受两个参数：`Immediate`和`Threshold`。`Immediate`决定拖动操作是否立即开始。在这种情况下，该方法在`OnMouseDown`中被调用。如果用户只是选择了某项而不想拖动它怎么办？将`Immediate`设置为`false`会延迟拖动操作的开始，直到鼠标移动了一定的像素数，该距离由`Threshold`属性决定。默认值为`-1`，在这种情况下距离由全局鼠标的`DragThreshold`属性设置。

> 提示：注意，方法没有使用`listBoxManager.BeginDrag(false)`，而是使用了通用的`(Sender as TListbox).BeginDrag(false)`。请记住，此应用程序中有多个列表框，用户可以将项目拖到屏幕上，此事件处理程序被编写为供所有列表框使用。

## 接受/拒绝被拖放的控件

当选中的项目被拖到其他控件上时，每个控件必须决定是否会“接受”被拖放的对象。控件可能接受或不接受有很多种原因。在接受控件的`OnOver`事件中，必须做出决定。如下：

```pascal
procedure TrmEmployee.ManagerDragOver(Sender, Source; X, Y: Integer; State: DragState);
begin
  Accept := (Source as TListBox).Parent = pnlDraggable;
end;
```

`OnDragOver`接收多个参数来描述触发事件的状况。有两个参数值得注意。`Source`决定了正在拖动的控件。`State`是`DragState`类型。`State`提供了更精确的视图。它可以是三个值之一。

### 表 15-5

| 值 | 说明 |
| --- | --- |
| `dsEnter` | 鼠标进入控件边界 |
| `dsMove` | 鼠标在控件上移动 |
| `dsLeave` | 鼠标移出控件边界 |

最后，`Accept`参数用于指定控件的决定。注意它是按引用传递的。这意味着它所持有的值将被应用。在这种情况下，如果`Source`是位于面板上的`ListBox`，则将`Accept`设置为`true`。

> 提示：在实现拖放时，`Sender`参数经常让开发者感到困惑。请记住`Sender`指定的是引发事件的组件，并不特定于拖放操作。它不决定“谁在发送移动”。该职责留给`Source`参数，即“对象的源”。

## 控件被释放时的操作

最后，当对象被释放时，接收控件必须决定对其进行什么。这发生在`OnDragDrop`事件中。

```pascal
procedure TfrmEmployee.ManagerDragDrop(Sender, Source: Object; X, Y: Integer);
begin
  editManager.Text := (Source as TListBox).Items[(Source as TListBox).Index];
end;
```
