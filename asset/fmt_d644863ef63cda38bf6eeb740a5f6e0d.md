
# Inkscape 扩展开发：创建“抖动”动画

Inkscape 中的任何对象都可以被分解为一组路径，而路径反过来又是由一组节点组成的。因此，修改任何对象的关键在于修改它的节点。

## 理解节点与控制点

什么是节点呢？你可能认为它是路径上可以改变方向的点。事实上，那只是一个给定的路径——例如一段文本——为了移动它的控制点，节点由三个控制点组成。

*   **控制点 0**：顶部的句柄。
*   **控制点 1**：在曲线上。
*   **控制点 2**：底部的句柄。

如果你从底部到顶部画（见图 1），顺序将反过来。同样，如果你从左到右画，第一个控制点在左侧；而从右到左画，则默认第一个控制点在右侧。当然，你可以抓住控制点并将它们移动到任何地方。

> **注意**：当你稍微移动节点，保存结果，再多移动一点，再次保存，以此类推。当你将这些帧组合在一起时，它会产生文字在抖动的印象。

在上个月的期刊[1]，我们看到了如何编写一个扩展来在 `Inkscape` 文档中渲染一个对象（圆形）。但除了创建新对象外，`Inkscape` 扩展还可以用于修改现有对象。让我们看看如何实现这一点，创建一个生成“抖动”动画的扩展。

## 实现“抖动”动画

主意是取一条路径并稍微移动它的控制点。如果你在某种程度上用过 `Inkscape`，你将熟悉这一点：绘制一条从顶部到底部由线段组成的贝塞尔曲线。使用编辑工具，选择节点（`Ctrl+A`）并使用工具栏使线段变得弯曲。

### 开发环境与文档

为了更清晰起见，解释如何创建此类脚本对于一个可以通过相对简单的脚本完成的任务来说似乎是一项大量工作。不幸的是，文档和教程是不存在的。同样，唯一的路是钻研源代码和注释，试图弄清楚可以使用哪些工具来实现我们的目标。

将 `CPS` 扩展保存到您的 `$HOME/.config/inkscape/extensions` 目录下。当您下次启动 `Inkscape` 时，该扩展将出现在 **扩展 (Extensions) | 修改路径 (Modify Path)** 菜单下。

例如，如果您在扩展对话框的 `CPS0` 字段中输入 `5`，则所选路径中所有节点的第一个句柄将向下并向右移动五个像素、毫米，或您正在使用的任何单位，相对于它们所示的原始位置。

*   位置 `(0, 0)` 位于 `Inkscape` 页面左上角。
*   `x` 坐标加上五表示向右五个单位。
*   `y` 坐标加上五表示向下五个单位。

### Jitter Nodes 扩展

这就是 `Jitter Nodes` 扩展所做的。该扩展默认随 `Inkscape` 一起发布，你可以在 `/usr/share/inkscape/extensions` 目录中找到它的代码。事实上，`jitter.py` 是 `Tremble` 的灵感来源（阅读“我完全直白地抄袭了它”），我在列表 3 和 4 中展示了我的扩展。

`Tremble` 是让所选对象产生抖动、摇晃动画的扩展。

## 配置扩展 (INX 文件)

`INX` 文件 `tremble.inx`（列表 3）非常标准。它允许你决定应用到每个节点的抖动幅度、生成多少帧以及将帧保存在哪里。

**列表 3: `tremble.inx`**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<inkscape-extension xmlns="http://www.inkscape.org/namespace/">
    <name>Tremble</name>
    <param name="radius" type="float" gui-text="Radius:1"/>
    <param name="accumulate" type="bool" gui-text="Accumulate wobble. changes">false</param>
    <param name="frames" type="int" gui-text="Frames:" min="1" max="250"/>
    <param name="folder" type="path" gui-text="Save frames in:" mode="folder"/>
    <effect>
        <object-type>path</object-type>
        <effects-menu>
            <submenu name="Modify Path"/>
        </effects-menu>
    </effect>
    <script>
        <language>python</language>
        <location>local</location>
        <descripion>Tremble a path</descripion>
        <name>Tremble</name>
        <short-descripion>Apply a random offset to a path's nodes</short-descripion>
        <script>tremble.py</script>
    </script>
</inkscape-extension>
```

*   `path` 参数允许用户输入或选择文件（`mode="file"`）或文件夹（`mode="folder"`），以便将其加载到 `Inkscape` 或稍后将内容保存到磁盘。
*   你可以给用户同时打开多个文件（`mode="files"`）或文件夹（`mode="folders"`）的选项。
*   或者创建一个文件（`mode="file_new"`）或文件夹（`mode="folder_new"`）。

## 核心脚本 (Python)

执行实际工作的脚本 `tremble.py`（列表 4）也不复杂。在头部，你导入了 `Inkscape` 的 `inkex` 模块，它包含了编写扩展所需的许多方法和属性。你还需要使用 Python 的 `random` 模块，并使用 `Inkscape` 命令模块中的某些内容。

**列表 4: `tremble.py`**

```python
#!/usr/bin/env python
## coding=utf-8

import random
import inkex
from inkex import command

class Tremble(inkex.EffectExtension):

    def add_arguments(self, pars):
        pars.add_argument("--radius", type=float, default=1, help="Radius")
        pars.add_argument("--frames", type=int, default=1, help="Frames")
        pars.add_argument("--folder", type="str", help="folder")
        pars.add_argument("--accumulate", type="bool", default=False, help="Accumulate")

    def effect(self):
        for node in self.tree.get_nodes():
            path = node.path
            for frame in range(self.options.frames):
                # ... 逻辑实现 ...
                # 脚本随后会将 svg 对象保存到文件夹节点中，
                # 你只需要跳过对它的操作并退出
```

### 节点操作逻辑

所选路径中的每个节点（行 24 到 29）都有一个 `x` 和一个 `y` 坐标。

*   控制点 0 的坐标为 `csp[0][0]` 和 `csp[0][1]` (`y` 坐标)。
*   操作示例：
    ```python
    csp[0][0] += self.options.CPS0
    csp[0][1] += self.options.CPS0
    csp[1][0] += self.options.CPS1
    csp[1][1] += self.options.CPS1
    csp[2][0] += self.options.CPS2
    csp[2][1] += self.options.CPS2
    ```

*   更新路径：
    ```python
    node.path = path
    ```

*   执行入口：
    ```python
    if __name__ == '__main__':
        CPS().run()
    ```

### 图片说明

*   **图 1**：一个节点由三个控制点组成：路径改变处的控制点是贝塞尔曲线上的节点之一。
*   **图 2**：`CPS` 扩展将帮助您确定方向以及定义该点曲率的两个句柄。注意位置 `(0, 0)` 位于 `Inkscape` 页面左上角。

*LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM*
*ISSUE 240 - 2020年11月 - 85*
*Linux Voice 教程 – TREMBLE（抖动）*
