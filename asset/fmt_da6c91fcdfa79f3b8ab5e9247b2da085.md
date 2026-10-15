
![](img/681a495129beb6adf91e7ff7f87e7dd4_608_0.png)

# 594 用户用户界面编程
## 第四部分

`ChatJFC` 程序与 `ChatAWT` 程序非常相似。我通过复制 `ChatAWT` 程序并执行以下操作编写了 `ChatJFC` 程序：

- 添加 `import swing (JFC)` 程序包语句。
- 将 `Label` 改为 `JLabel`，将 `Button` 改为 `JButton` 等。
- 在需要的地方使用 `getContentPane` 方法获取用于添加组件的内部容器，并将布局管理器设置为 `null`。

# 使用原生 Java 编译器

有两个正在开发中的原生 Java 编译器，一个是 `Towerj` (`www.towerj.com`)，另一个是 `Cygnus` (`www.cygnus.com`)。在本章编写时（1999 年 3 月），`Cygnus` 编译器仅在早期测试发布版本中可用，但它看起来很有前景。`Towerj` 编译器是一个商业产品。我已经用它运行了三个程序，并看到与使用 `JIT`（即时编译）相比，性能有了 4 倍到 11 倍的提升。Java 的优点之一是其字节码的可移植性。然而，对于服务器端程序，放弃可移植性以换巨大的性能提升通常是一个不错的选择。

### 总结

这个简短的章节希望让你快速了解了 Java 语言，并激发你进一步学习该语言的动力。互联网上有许多关于 Java 编程的信息源。由于网站会发生变化，我将在我的网站（`www.markwatson.com/books/linux_prog.html`）上保留我喜爱的 Java 资源链接。

这个简短的章节没有涵盖许多有趣的话，例如：

- 绘制图形
- 编写处理用户界面事件的 applet
- 为 C 或 C++ 程序员提供的技巧

如果你是 C 或 C++ 程序员，我敦促你也学习 Java。我已经使用 C 语言 15 年，C++ 10 年，但在大多数开发工作中我更倾向于使用 Java。确实，Java 程序的运行速度会比同类的 C 或 C++ 程序慢。然而，在使用 Java 大约 3 年后，我相信 Java 能让我用编写相同 C++ 应用程序所需时间的一半写出一个大型应用程序。我与其他开发者交流过，他们同意在 Java 中编程的效率大约是 C 或 C++ 的两倍。

---

# OpenGL/Mesa 图形编程

作者：Mark Watson

### 本章内容

- OpenGL 是图形图形硬件的软件接口 596
- Orbits 示例程序 597

## 33 章节

# 用户用户界面编程
## 第四部分

`OpenGL` API 由 Silicon Graphics 开发，并已成为高质量 3D 图形的行业标准。尽管有 `OpenGL` 的 Linux 商业移植版，但由 Brian Paul 编写了一个高质量的、公有领域的、类 `OpenGL` 实现—— `Mesa`。`Mesa` 不能称为 `OpenGL`，因为没有获得 Silicon Graphics 的授权，但我发现它是 Linux 上进行 `OpenGL` 编程的有效工具。`Mesa` 可能会包含在你的 Linux 发行版中。尽管你已经安装并正在使用 `Mesa`，我将在本章中仍提到 `OpenGL`。我会在我的网站上保留 `Mesa` 发行版的最新链接。

`OpenGL` API 非常复杂。我们将在本章中使用一个示例来说说明如何使用 `OpenGL` 辅助库来绘制简单形状，并在程序控制下放置和旋转形状。我们还将学习如何使用光照效果以及如何更改视角。

# OpenGL 是图形图形硬件的软件接口

# Orbits 示例程序

已成为高质量 3D 图形的行业标准。作者：Mark Watson

(`www.angel.com`)，我们在那里使用专有软件在各种硬件（包括 Nintendo Ultra64、Windows 和 SGI 工作站）上渲染实时 3D 图形。这种专有软件作为选项，使用 `OpenGL` 与图形硬件通信。

X 坐标向右逐渐增加，Y 坐标向上移动，z 坐标向屏幕内部深度增加。原点（例如 X=Y=Z=0 处）位于屏幕中心。

# 用户界面的编程
## 第四部分

图 33.1 显示了在默认平滑着色模式下运行的示例程序。此图的背景颜色已改为白色；CD 光盘上的程序背景为黑色。

图 33.1
以平滑着色运行的轨道程序。

![](img/681a495129beb6adf91e7ff7f87e7dd4_613_0.png)

# 为 OpenGL 图形创建窗口并初始化 OpenGL

在本章中，我们将使用 OpenGL 实用库函数初始化 OpenGL、`GLUT` 库，并为绘图创建一个窗口：

| 函数 | 描述 |
|---|---|
| `glutinit` | 初始化 GLUT 和 OpenGL。 |
| `glutInitDisplayMode` | 设置显示属性（我们的示例程序将设置允许双缓冲、深度缓冲和使用 RGB 颜色的属性）。 |
| `glutInitWindowSize` | 设置主窗口的大小。 |
| `glutInitWindowPosition` | 设置主窗口在桌面或 X Windows 显示器位置。 |
| `glutCreateWindow` | 实际创建主窗口。 |

# OpenGL/Mesa 图形编程 第33 章

示例程序中的初始化代码如下：

在调用 `glutInitDisplayMode` 时，我们使用以下常量：

| 常量 | 描述 |
|--- | --- |
| `GL_DOUBLE` | 启用双缓冲以实现平滑动画。 |
| `GL_RGB` | 指定使用 RGB 色彩板。 |
| `GL_DEPTH` | 启用深度缓冲以确定场景中一个物体何时遮挡另一个物体。 |

# 使用 GLUT 创建 3D 对象

有几个 `GLUT` 实用函数可以创建线框模型和实体对象。要创建一个球体，请使用以下任意一种：

```
void glutSolidSphere(GLdouble radius, GLint slices);

void glutWireSphere(GLdouble radius, GLint stacks);
```

在这里，`radius` 是球体的半径。`slices` 参数是环绕 z 轴的平面带数量。数值越高，球体越越平滑。`stacks` 参数是沿 z 轴的平面带数量。较小的 `slices` 和 `stacks` 值会产生所绘制的形状。球体是在建模坐标系的原点中心绘制（或渲染）的（例如，使用 OpenGL 模式处于建模模式；或之后）。

要创建一个立方体，请使用以下任意一种：

```
void glutSolidCube(GLdouble size);

void glutWireCube(GLdouble size);
```

`size` 参数是立方体任意边的边的长度。

要绘制一个锥体，请使用以下任意一种：

```
void glutSolidCone(GLdouble base, GLdouble height, GLint slices, GLint stacks);

void glutWireCone(GLdouble base, GLdouble height, GLint slices, GLint stacks);
```

`base` 参数是锥底的半径。`height` 参数是锥体的高度。`slices` 参数是环绕 z 轴绘制的平面带数量。`stacks` 参数是沿 z 轴绘制的平面带数量。锥底的中心位于建模系统的 X=Y=Z=0 。如果你想绘制一个圆环，请使用以下 `GLUT` 函数之一：

```
void glutSolidTorus(GLdouble inner_radius, GLdouble outer_radius, GLint nsides, GLint rings);

void glutWireTorus(GLdouble inner_radius, GLdouble outer_radius, GLint nsides, GLint rings);
```

`inner_radius` 和 `outer_radius` 参数是圆环的内、外半径。`nsides` 参数是每个径向部分绘制的平面带数量。`rings` 参数是平面带的数量。

# 在 3D 空间中放置对象

在将对象放置于 3D 世界之前，我们需要确保 OpenGL 处于建模模式。这通过调用以下函数实现：

```
glMatrixMode(GL_MODELVIEW)
```

我们可以通过调用以下函数将模型世界的原点平移到坐标 X、Y 和 Z：

```
glTranslate(GLfloat X, GLfloat Y, GLfloat Z);
```

当我们移动了原点时，我们记得一个问题：幸运的是，有 OpenGL 函数可以确保 OpenGL 的整个状态保存到栈中，并能从栈中取出状态。这些函数是：

```
glPushMatrix();

glPopMatrix();
```

在在实践中，我们通常会推入“矩阵”（例如 OpenGL 的状态），对一个或多个对象执行操作，然后将“矩阵”从栈中弹出。示例展示了如何绘制一个半径为 1.0 的球体到 X=10, Y=0.0, 和 Z=1.0：

```
glPushMatrix();
{
```
