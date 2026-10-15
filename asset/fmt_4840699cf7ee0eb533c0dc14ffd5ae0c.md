
# style `<name>` = `<name>`

```
# {
#   <option>
#}
#
# widget <widget_set> style <style_name>
# widget_class <widget_class> style <style_name>
```

```
style="ruler"
{
  font = "adobe-helvetica-medium-r-normal-*-80-*:*:*:*:*:*"
}

style="default"
{
  font = "adobe-helvetica-medium-r-normal-*-100-*:*:*:*:*:*"
}

widget_class="Ruler" style="ruler"
widget_class="class" style="default"
```

另一个 `gtkrc` 文件² 包含在 GIMP 源码目录下。名为 `gtkrc.forest2`。它看起来类似于下所示：

```
# style <name> = <name>
# {
#   <option>
#}
#
# widget <widget_set> style <style_name>
# widget_class <widget_class> style <style_name>

pixmap_path="/home/tiger/.gnome/textures
```

> ² `gtkrc.forest2` 是由著名的 Gimp'er tiger 创建的。

```
style 'default'
{
# font = '-schumacher-clean-medium-r-normal-80-75-c-50-iso8859-1'
font = '-.lucida-medium-r-normal-10-.*.*-iso8859-1'

# base, text, bg, fg are possible
bg[NORMAL] = { 0.70, 0.75, 0.35 }
bg[SELECTED] = { 0.31, 0.35, 0.35 }
bg[INENSITIVE] = { 0.70, 0.75, 0.67 }
bg[ACTIVE] = { 0.61, 0.65, 0.58 }
bg[PRELIGHT] = { 0.84, 0.89, 0.81 }

fg[NORMAL] = { 0.0, 0.0, 0.0 }
fg[SELECTED] = { 0.9, 0.9, 0.0 }
fg[ACTIVE] = { 0.33, 0.2, 0.0 }
fg[PRELIGHT] = { 0.5, 0.1, 0.0 }

text[INENSITIVE] = { 0.60, 0.65, 0.57 }

}
```

```
style 'ruler'
{
font = '-adobe-helvetica-medium-r-normal-*-80-.*.*...*.*'
}
```

```
widget_class "Ruler" style 'ruler'
widget_class "" style 'default'
```

如果你想使用你的 tiger `gtkrc`，请将其复制到你的 `.gimp/gtkrc` 文件中，当你重启 GIMP 时，它将采用那种样式。

外观是通过在 `gtkrc` 文件中创建各种“样式（styles）”控制的。这些样式遵循这种格式：

```
style 'name'
{
# 配置信息
}
```

在样式部分，有几个可以更改的不同选项。字体是通过类似于这样的线性选择的：

```
font = '-adobe-helvetica-medium-r-normal-*-80-.*.*..*.*.'
```

此示例使用了 Adobe Helvetica 字体。具体的字体信息可以通过程序 `xfontsel` 选择。

下一组受影响的选项涉及颜色。颜色使用如下百分比值进行选择：

```
Attribute[STATE] = { Red, Green, Blue }
```

颜色有三个属性：

- `fg`. 前景颜色。
- `bg`. 背景颜色。
- `text`. 文本颜色。

在这些每一个属性中，有五种这些属性可以存在的状态：

- `NORMAL`。属性的正常颜色。
- `PRELIGHT`。当光标悬停在上方时，属性的颜色。
- `ACTIVE`。当点击鼠标按钮时，属性的颜色。
- `INSENSITIVE`。当无法点击时，属性的颜色。
- `SELECTED`。被选中时，属性的颜色。

然后必须将样式应用于一组小组件。可以使用通配符来指定多个小组件。在所有小组件上使用“default”样式，它看起来类似于这样：

```
widget_class "default"
```
