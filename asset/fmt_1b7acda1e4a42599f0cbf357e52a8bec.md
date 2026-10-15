
```python
############################################################
# proc toolbar {name args}
# 点击时执行command
# 参数
# name      toolbar的名字
# args      -flag 值对列表
# 结果
# 创建一个新的toolbar并返回name
# 如果缺少必需的参数则抛出错误
proc toolbar {name args} {
    # 这些参数是必需的
    set reqOptions [list -command -image]

    # 检查必需参数是否存在
    foreach required $reqOptions {
        if ![lsearch exact $args $required] {
            error "toolbutton requires a $required option"
        }
    }

    # defaults
    set height 32
    set width 32
    set background gray80
    set foreground black

    # 遍历参数
    # 确认每个选项都是有效的，
    # 为每个定义的选项设置变量。
    set validOptions [list -command -info -height -width]
    foreach option $args {
        if ![lsearch exact $validOptions $option] {
            error "Bad $option must be one of $validOptions"
        }
        set item [string range $option 1 end]
        eval [set $item $val]
    }

    # 为toolbutton创建canvas
    canvas $name -height $height -width $width -background $background
    # 将图像放在其中
    $name create image [expr $height/2] [expr $width/2] -image $image

    # 绑定点击执行全局作用域内的command
    bind $name <ButtonPress-1> [list $command]
    # 鼠标进入时更改背景
    bind $name <Enter> "$name configure -background $highlight"
    # 鼠标离开时更改背景。取消任何挂起的标签显示。
    bind $name <Leave> "$name configure -background; catch {cancel [namespace current::toolButton::after $info]}"
    # 当按钮移动时，重置任务
    bind $name <Motion> "[namespace current::toolButton::scheduleInfo $info]"

    # 返回name
    return $name
}

frame .f
pack .f
set question [image create bitmap -data {
#define question_width 20
#define question_height 22
static unsigned char question_bits[] = {
0xf8, 0x1f, 0x00, 0xac, 0x2a, 0x00, 0x56, 0x55, 0x00, 0xeb, 0x00,
0xf5, 0x0f, 0x01, 0xfb, 0xbf, 0x00, 0x75, 0x0d, 0x01, 0xfb, 0xbe, 0x02,
0x75, 0x0d, 0x05, 0xab, 0xbe, 0x0a, 0x55, 0x0f, 0x07, 0xab, 0x00,
0xd6, 0x57, 0x01, 0xac, 0xab, 0x00, 0xd8, 0x57, 0x00, 0xb0, 0xaa, 0x00,
0x50, 0x55, 0x00, 0xb0, 0x0b, 0x00, 0xd0, 0x17, 0x00, 0xb0, 0x0b, 0x00,
0x58, 0x15, 0x00, 0xa8, 0x2a, 0x00;
}}
set questhd [image create bitmap -data {
#define questhead_width 19
#define questhead_height 21
static unsigned char questhead_bits[] = {
  0xff, 0xff, 0x07, 0x55, 0x55, 0x05, 0xa2, 0x2a, 0x03, 0x66,
  0x15, 0x01,
  0xa2, 0x2a, 0x03, 0x66, 0x15, 0x01, 0xc2, 0x0a, 0x03, 0x03, 0x46,
  0x05, 0x01,
  0x82, 0x0a, 0x03, 0x06, 0x05, 0x01, 0x02, 0x03, 0x03, 0x86,
  0x05, 0x01,
  0xc2, 0x0a, 0x03, 0x66, 0x15, 0x01, 0xa2, 0x2a, 0x03, 0x66,
  0x15, 0x01,
  0xa2, 0x2a, 0x03, 0x66, 0x15, 0x01, 0xa2, 0x2a, 0x03, 0xff,
  0x05, 0x07,
  0xab, 0xaa, 0x02;
}}
set warning [image create bitmap -data {
#define warning_width 6
#define warning_height 19
static unsigned char warning_bits[] = {
0x0c, 0x16, 0x2b, 0x15, 0x2b, 0x15, 0x2b, 0x16, 0x0a, 0x16,
0x0a, 0x16,
0x0a, 0x00, 0x00, 0x1e, 0x0a, 0x16;
}}
```

- 可以使用 `canvasName coords` 命令访问或修改可绘制项的坐标。

  语法：`canvasName coords tagOrId ?x1 y1? ... xn yn?`

- 可以使用 `canvasName` 命令在画布上移动可绘制项。

  语法：`canvasName move tagOrId xoffset yoffset`

- 通过 `canvasName bbox` 命令返回可绘制项占据的空间。

  语法：`canvasName bbox tagOrId`

- 通过 `canvas-Name find` 命令返回符合搜索标准的项项列表。

  语法：`canvasName find searchSpec`

- 可以使用 `canvasName raise` 命令和 `canvasName lower` 命令修改可绘制项在显示列表中的位置。

  语法：`canvasName raise tagOrId ?abovetagOrId?`

  语法：`canvasName lower tagOrId ?belowtagOrId?`

- 通过 `font families` 命令返回可用字体列表。

  语法：`font families ?-displayof windowName`

- 通过 `font measure` 命令返回在特定字体中显示字符串所需的水平空间。

  语法：`font measure font ?-display windowName? text`

- 通过 `font actual` 命令返回与请求字体最匹配的字体。

  语法：`font actual font ?-displayof windowName?`

- 可以使用 `bind` 命令将动作绑定到组件的事件上。

  语法：`bind widgetName eventType script`

- 可以使用 `canvasName bind` 将动作绑定到画布组件内可绘制项的事件上。

  语法：`canvasName bind tagOrId eventType script`

## 9.8 底部总结

可以使用 `image create` 命令创建双色（位图）和多色（照片）图像。

语法：`image create type ?name? ?options?`

- 可以使用 `image delete` 命令删除图像。

  语法：`image delete name ?name?`
