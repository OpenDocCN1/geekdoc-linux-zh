
```python
gradient = QLinearGradient(QPointF(0, 0), QPointF(0, 100))
gradient.setColorAt(0, Qt.white)
a = self.leftSpinBox.value()
gradient.setColorAt(1, Qt.red if a != 0 else Qt.white)
painter.setBrush(QBrush(gradient))
painter.drawPolygon(
    QPolygon([(ax, ay, bx, by, cx, cy, ix, iy)]))
```

对于代表左侧 spinbox 的“Y”形结构的左侧部分——形状 `(a, b, c, i)`——我们使用从白色到红色的线性颜色渐变。

```python
gradient = QLinearGradient(QPointF(0, 0), QPointF(0, 100))
gradient.setColorAt(0, Qt.white)
b = self.rightSpinBox.value()
gradient.setColorAt(1, Qt.blue if b != 0 else Qt.white)
```

### 表 11.3 选定的 QPainter 绘图相关方法

| 语法 | 描述 |
| :--- | :--- |
| `p.drawArc(r, a, s)` | 在由 `QRect` `r` 包围的圆上，从角度 `int` `a`° 开始，跨越 `s`°，在 `QPainter` `p` 上绘制一段圆弧 |
| `p.drawChord(r, a, s)` | 在由 `QRect` `r` 包围的圆上，从角度 `int` `a`° 开始，跨越 `s`°，在 `QPainter` `p` 上绘制一条弦 |
| `p.drawConvexPolygon(pl)` | 在 `QPainter` `p` 上绘制一个凸多边形，连接 `pl` 中 `QPoints` 列表中的所有点，并将最后一个点连接回第一个点 |
| `p.drawEllipse(r)` | 在 `QPainter` `p` 上绘制一个由 `QRect` `r` 包围的椭圆；如果 `r` 是正方形，则绘制一个圆 |
| `p.drawImage(pt, i)` | 在 `QPoint` `pt` 处，在 `QPainter` `p` 上绘制 `QImage` `i`；不同的参数允许只绘制图像的一部分 |
| `p.drawLine(p1, p2)` | 在 `QPainter` `p` 上绘制 `QPoints` `p1` 和 `p2` 之间的一条线。有许多参数变体；还有 `drawLines()` 方法。 |
| `p.drawPath(pp)` | 在 `QPainter` `p` 上绘制 `QPainterPath` `pp` |
| `p.drawPie(r, a, s)` | 在由 `QRect` `r` 包围的圆中，从角度 `int` `a`° 开始，跨越 `s`°，绘制一个扇形 |
| `p.drawPixmap(pt, px)` | 在 `QPoint` `pt` 处，在 `QPainter` `p` 上绘制 `QPixmap` `px`；不同的参数允许只绘制 pixmap 的一部分 |
| `p.drawPoint(pt)` | 在 `QPainter` `p` 上绘制 `QPoint` `pt`；还有 `drawPoints()` 方法 |
| `p.drawPolygon(pl)` | 在 `QPainter` `p` 上绘制一个多边形，连接 `pl` 中 `QPoints` 列表中的所有点，并将最后一个点连接回第一个点 |
| `p.drawPolyline(pl)` | 在 `QPainter` `p` 上绘制一条多段线，连接 `pl` 中 `QPoints` 列表中的所有点；不将最后一个点连接回第一个点 |
| `p.drawRect(r)` | 在 `QPainter` `p` 上绘制一个 `QRect` `r` |
| `p.drawRoundedRect(r, x, y)` | 在 `QPainter` `p` 上绘制一个由 `QRect` `r` 包围的圆角矩形，使用整型 `x` 和 `y` 作为圆角因子 |
| `p.drawText(r, s, o)` | 在 `QRect` `r` 范围内，在 `QPainter` `p` 上绘制字符串 `s`，并使用可选的 `QTextOption` `o` |
| `p.drawText(x, y, s)` | 在点 `(x, y)` 处，在 `QPainter` `p` 上绘制字符串 `s` |
| `p.fillPath(pp, b)` | 使用 `QBrush` `b` 填充 `QPainter` `p` 上的 `QPainterPath` `pp` |
| `p.fillRect(r, b)` | 使用 `QBrush` `b` 填充 `QPainter` `p` 上的 `QRect` `r` |
| `p.setBrush(b)` | 将填充形状的画刷设置为 `QBrush` `b` |
| `p.setPen(pn)` | 将线条和轮廓的画笔设置为 `QPen` `pn` |
| `p.setFont(f)` | 将 `QPainter` `p` 的文本字体设置为 `QFont` `f` |

```python
painter.setBrush(QBrush(gradient))
painter.drawPolygon(
    QPolygon([cx, cy, dx, dy, ex, ey, fx, fy]))
```

右半部分——形状 `$(d, e, f, c)$`——与左半部分非常相似，只是它使用的渐变从白色过渡到蓝色。

```python
if (a + b) == 0:
    color = QColor(Qt.white)
else:
    ashare = (a / (a + b)) * 255.0
    bshare = 255.0 - ashare
    color = QColor(ashare, 0, bshare)
    gradient = QLinearGradient(QPointF(0, 0), QPointF(0, 100))
    gradient.setColorAt(0, Qt.white)
    gradient.setColorAt(1, color)
    painter.setBrush(QBrush(gradient))
    painter.drawPolygon(
        QPolygon([cx, cy, fx, fy, gx, gy, hx, hy, ix, iy]))
```

“Y”形的茎部——形状 `$(c, f, g, h, i)$`——使用线性渐变绘制，该渐变从白色过渡到一种红色/蓝色，其颜色比例与左侧/右侧的流速成正比。

```python
painter.setPen(Qt.black)
painter.drawPolyline(QPolygon([ax, ay, ix, iy, hx, hy]))
painter.drawPolyline(QPolygon([gx, gy, fx, fy, ex, ey]))
painter.drawPolyline(QPolygon([bx, by, cx, cy, dx, dy]))
```

最后，我们绘制代表管道侧边的线条。第一条线在左侧从 `$a$` 到 `$i$`，勾勒出管道的左边缘；第二条线从 `$g$` 到 `$f$` 再到 `$e$`，勾勒出管道的右边缘；第三条线从 `$b$` 到 `$c$` 再到 `$d$`，标出顶部的“V”形部分。

与 PyQt 内置小部件一样，`YPipeWidget` 和 `Fraction-Slider` 都可以用作顶级小部件，这在开发和测试自定义小部件时特别有用。`chap11/fractionslider.py` 和 `chap11/ypipewidget.py` 都可以作为独立程序运行，因为这两个文件在 `QWidget` 子类之后都有 `if __name__ == "__main__":` 语句，并包含创建 `QApplication` 以及创建并显示自定义小部件的代码。

## 总结

PyQt 提供了多种自定义小部件外观和行为的方法。最简单且最常用的方法是设置现有小部件的属性为我们想要的值。从 Qt 4.2 开始，样式表（style sheet）属性可用，通过简单的纯文本输入并使用 CSS 语法，我们就能对小部件的外观产生显著影响。样式表的一个常见且非常容易使用的用途是设置强制小部件（mandatory widgets）的背景颜色。

复合小部件允许我们将两个或更多的小部件布局在一起，并将结果小部件视为单个小部件。如果复合小部件被大量使用，这将节省时间，并且为在主窗口风格应用程序的中心区域拥有多个小部件提供了一条途径。一些程序员将组成小部件设为私有并转发它们的信号和槽，但在许多情况下，最简单的方法是将组成小部件保留为公共实例变量，并直接访问和连接它们。

对现有小部件进行子类化以调整其外观，尤其是行为，比创建 `QWidget` 子类并自己处理一切要容易得多。这种方法适用于几乎每一种 PyQt 小部件，因为大多数小部件都是设计为可被子类化的。这种方法的唯一局限性是，它只能应用于那些与我们想要的小部件足够相似，从而使调整可行的其他小部件。
