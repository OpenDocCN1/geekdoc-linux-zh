
- `display`：指定到 X 服务器的连接。
- `w`：指定窗口。
- `text_prop_return`：返回 `XTextProperty` 结构。

`XGetWMClientMachine` 方便函数对 `WM_CLIENT_MACHINE` 属性执行 `XGetTextProperty`。成功时返回非零状态；否则返回零状态。

## 标准调色板 (Colormaps)

带有调色板、平滑阴影绘制或数字化图像的应用需要大量的颜色。此外，这些应用程序通常需要一种从颜色三元组到像素值的有效映射，以显示适当颜色。

例如，考虑一个想要绘制平滑阴影球体的三维显示程序。在程序图像的每个像素处，程序计算反射回观察者的光强度和颜色。每次计算的结果是一个红、绿、蓝（RGB）三元组，范围在 0.0 到 1.0 之间。为了绘制球体，程序需要一个提供大量均匀分布颜色的调色板。该 `col` 应该是一个提供大量均匀分布颜色的调色板。

# 客户端间通信函数

```
(r * red_mult + g * green_mult + b * blue_mult + base_pixel) & 0xFFFFFF
```

对于灰度（GrayScale）调色板，定义了 `colormap`、`red_max`、`red_mult` 和 `base_pixel`。其他成员均被忽略。计算灰度像素值时使用以下表达式：

```
(gray * red_mult + base_pixel) & 0xFFFFFF
```
