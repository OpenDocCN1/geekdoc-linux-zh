
...是将常量 100 替换为变量 `self.options.radius` 并将其转换为字符串，这正是 inkex 的 `Circle` 方法所期望的。

你还可以使用许多其他类型的参数来构建其他复杂的对话框。例如，布尔参数（boolean parameter）会生成一个复选框来设置 true/false 值。你可以将默认值设置为 true 或 1，或者 false 或 0。`optiongroup` 参数会生成一组单选按钮，你可以从中选择一个预定义的值 —— 不同的选项是通过 `<option>` 元素创建的。

幸运的是，这是一个拥有良好文档的领域，因此你可以阅读关于可以使用的不同类型字段的介绍 [1]。

**图 2：在你的 .inx 文件中添加 `<param> ... </param>` 会生成一个对话框，你可以在其中设置字段 – 在此情况下，是圆的半径。查看列表 5 (Listing 5) 以获取这些字段的实际效果概述。**

2020年10月 | 第239期
LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM

## 教程 – INKSCAPE 脚本 Linux 之声

### 列表 4：draw_circle.py (l)

一个允许你输入圆数值的文本框，但你已经在上面的示例中见过了。

```python
#!/usr/bin/env python
## coding=utf-8
import inkex
from inkex import Circle
def effect(self):
    parent = self.svg.get_current_layer()
    style = {'style': '#000000', 'stroke-width': 1, 'fill': '#FF0000'}
    circle_attrs = {'style': str(inkex.Style(style)), 'cx': '100', 'cy': '100', 'r': str(self.options.radius)}
```

第 9 行到第 13 行以及第 15 行到第 19 行执行了一些有趣的操作（图 3）。假设你想为用户提供一些选项，让他们选择圆在页面上的位置 – 右侧；以及页面顶部、中间或底部。这是 `optiongroup` 派上用场的情况之一，但你可以给它一个 `appearance="combo"` 选项。这会让选项以组合框（下拉菜单）的形式出现。

```python
    inkex.addNS('label', 'inkscape'):
    parent.add(Circle (**circle_attrs))
if __name__ == '__main__':
    DrawCircle ().run()
```

`notebook` 小部件（第 21 行到第 28 行）创建一组可以包含其他部件的标签。你的用户可以在每个标签之间切换并在它们包含的字段中输入参数。在这个示例中，`notebook` 颜色选择器甚至带有一个颜色框。当然，你也可以让一个部件包含两个页面，每个页面上方都叠放着一个颜色框，但将它们放在 `notebook` 中更加优雅。颜色，一个用于圆的描边，另一个用于填充。如你在图 3 所示，这些颜色框非常完整，让你的用户不仅可以设置颜色，还可以设置……

另请注意，尽管 `notebook` 是其他部件的容器，但在处理输入时，你仍然需要从中捕获值。

## 列表 5：draw_circle.inx (II)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<inkscape-extension xmlns="http://www.inkscape.org/namespace/extension">
  <id>org.linuxmagazine.inkscape.effects.drawcircle</id>
  <name>Draw Circle</name>
  <page name="stroke" gui-text="Stroke">
    <param name="scolor" type="color" gui-text="Stroke Color:">255</param>
  </page>
  <page name="fill" gui-text="Fill">
    <param name="fcolor" type="color" gui-text="Fill Color.">255</param>
  </page>
  <param name="radius" type="int" min="1" max="1000" gui-text="Radius.">100</param>
  <param name="posx" type="optiongroup" appearance="combo" gui-text="Position x:">
    <option value="left">Left</option>
    <option value="center">Center</option>
    <option value="right">Right</option>
  </param>
  <param name="posy" type="optiongroup" appearance="combo" gui-text="Position y:">
    <option value="top">Top</option>
    <option value="center">Center</option>
    <option value="bottom">Bottom</option>
  </param>
  <param name="swidth" type="int" appearance="full" gui-text="Stroke width:" min="1" max="10">1</param>
  <effect>
    <object-type>path</object-type>
    <submenu name="Render"/>
    </submenu>
  </effect>
  <param name="tab" type="notebook">
    <script location="inx" interpreter="python">circle.py</script>
  </param>
</inkscape-extension>
```

2020年10月 | 第239期
LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM

从你脚本中的 inx 表单中获取。否则，当你点击“应用”时会得到错误。你将在下方看到如何进行操作。

在图 3 的底部，你有一个另一个整数的文本框，但使用 `appearance="full"` 选项（第 30 行，列表 5），你可以用来修改圆的描边。正如列表 5 所示，在 inx 表单中处理这些选项很容易的。列表 6 显示了如何完成的。尽管 `notebook` 小部件没有返回任何有用的参数，你仍然需要在第 22 行确认它。

**图 3**：多种类型的字段用于创建这个复杂的对话框，让用户设置属性 – 在这种情况下是圆的位置。第 22 行计算了圆的位置。

### 列表 6：draw_circle.py (II)

```python
#!/usr/bin/env python
## coding=utf-8
import inkex
from inkex import Circle
class DrawCircle(inkex.Extension):
    def add_arguments(self):
        pars.add_argument("--swidth", type=int, default=1, help="Stroke width")
    def effect(self):
        parent = self.svg.get_current_layer()
        if self.options.posx == "left":
            center_x = self.options.radius + (self.options.swidth/2)
        elif self.options.posx == "center":
            center_x = self.svg.width / 2
        else:
            center_x = self.svg.width - self.options.radius - (self.options.swidth/2)
        center_x = str(center_x)
        if self.options.posy == "top":
            center_y = self.options.radius + (self.options.swidth/2)
        elif self.options.posy == "center":
            center_y = self.svg.height / 2
        else:
            center_y = self.svg.height - self.options.radius - (self.options.swidth/2)
        center_y = str(center_y)
        style = {'style': self.options.scolor, 'stroke-width': str(self.options.swidth), 'fill': self.options.fcolor}
        circle_attrs = {'style': str(inkex.Style(style)), 'cx': center_x, 'cy': center_y, 'r': str(self.options.radius)}
        inkex.addNS('label', 'inkscape'): 'mycycle',
        parent.add(Circle (**circle_attrs))
if __name__ == '__main__':
    DrawCircle ().run()
```
