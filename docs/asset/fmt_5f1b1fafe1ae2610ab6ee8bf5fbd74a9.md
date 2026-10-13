
# 1026 Linux 编程

## 第四部分

### 列表 33.1 延续

```
proc make_preview {} {
  global color;
  frame .preview_frame;
  label .preview_label -bg $color \
  -height 5 -width 5;
  pack .preview_label -in .preview_frame \
  -padx 2 -pady 2 -fill both -anchor c \
  -expand 1;
  pack .preview_frame -in .control_frame \
  -side top -fill both -expand 1 \
  -padx 2 -pady 2;
}
```

```
proc make_buttons {} {
  frame .button_frame;
  button .apply -text "apply" -command setRootColor;
}
```

继续 ![](img/fbfff30e42d507bc7531108a281d6cf4_1062_0.png)

```
button .quit "quit" -command exit;
pack .apply -in .button_frame -fill both \
expand 1 -padx 2 -pady 2 -side left;
pack .button_frame -in .main_frame -fill both;

proc setRootColor {} {
    global color;

    catch {
        exec xsetroot -solid $color;
    }

    if {$msg} != "" {
        set msg "An ($msg) error occurred";
    } else {
        set msg "$color";
    }

    .message_label configure -text $msg;
}
```

### 总结

此过程是使用框架（`frames`）的良好示例。总之，这个示例创建了四个框架，为每个滑块和标签对创建一个，以及每一个框架。将标签和滑块添加到它们自己的框架中简化了整体布局策略。

此过程中的另一个示例是小组件的 `-command` 选项。每当比例尺（`scales`）变化时，就会执行 `-command` 选项指定的命令。在这种情况下，执行 `setColor` 命令，它设置了全局变量 `color`：

```
proc setColor {value}
  global color;
  foreach i {red blue} {
    set S {%format %02x [.scale_$i $i]}
  }
  set color "#redGreenSblue"
  preview_label configure -bg $color;
  message_label configure -text "Color";
}
```

你可以通过设置组件的背景颜色来预览颜色变化。`.preview_label`。使用以下过程创建 `.preview_label`：

```
proc make_preview {}
  global color;
  frame .preview_frame;
  label .preview_label -bg $color \
  -height 5 -width 5;
  pack .preview_label -in .preview_frame \
  -pad x 2 -fill both \
  -anchor c -expand 1;
  pack .preview_frame -in .control_frame \
  -side bottom -fill both -expand 1 \
  -pady 2 -pady 2;
}
```

现在你需要添加几个按钮——一个用于应用更改，另一个用于退出程序。使用以下过程：

```
proc make_buttons {}
  frame .button_frame;
  button .apply -text "apply" \
  -command setRootColor;
  button .quit -text "quit" -command exit;
  pack .apply -in .button_frame \
  -fill both -expand 1 -padx 2 \
  -pady 2 -side left;
  pack .button_frame -in .main_frame \
  -fill both;
}
```

![](img/fbfff30e42d507bc7531108a281d6cf4_1060_0.png)

# Linux 编程

## 第四部分

你还需要以下过程，它设置了根颜色：

```
proc setRootColor {} {
  global color;

  catch {
    exec xsetroot -solid $color;
    msg;
  };

  if {$msg} != "" {
    set msg "An ($msg) error occurred";
  } else {
    set msg "$color";
  }

  .message_label configure -text $msg;
}
```

现在你已经完成了这些过程，请调用它们：

```
make_message_label;
make_scales;
make_preview;
make_buttons;
```

你现在准备好测试你的小型 `tcl` 应用程序了。当应用程序运行时，生成的窗口应该像图 33.5 所示。

## 图 33.5

带有按钮和颜色的 `tksetroot` 窗口。

![](img/fbfff30e42d507bc7531108a281d6cf4_1061_0.png)

列表 33.1 包含了 `tksetroot` 应用程序的源代码。

# 列表 33.1 tksetroot

```
set color "#000000";
frame .main_frame;
frame .message_frame;
frame .control_frame;
```

```
pack .control_frame -in .main_frame -expand 1 fill both;
pack .main_frame -anchor c -expand 1;
pack .message_frame -anchor s -padx 2 -pady 2 \
-fill x -expand 1;
```

# tcl 和 tk 编程

## 第33 章 1025

```
proc make_message_label {} {
  label .message_label -relief sunken;
  pack .message_label -anchor c -in .message_frame \
  -padx 2 -pady 2 -fill both -expand 1;
}
```

```
proc make_scales {} {
  frame .scale_frame;
  foreach i {red green blue} {
    frame .scale_$i -bg $i;
    label .label_$i -text $i -bg $i -fg white;
    scale .scale_$i -from 0 -to 255 \
    -command setColor;
    pack .label_$i .scale_$i -in .scale_frame -side left
    pack .scale_$i -in .control_frame -side left \
    -padx 2 -pady 2;
  }
  pack .scale_frame -in .control_frame -side left -expand 1;
}
```

```
proc setColor {value} {
  global color;
  foreach i {red green blue} {
    set $i [format %02x [.scale_$i get]];
  }
  set color #$redgreenblue;
  .preview_label configure -bg $color;
  message_label configure -text "$color";
}
```
