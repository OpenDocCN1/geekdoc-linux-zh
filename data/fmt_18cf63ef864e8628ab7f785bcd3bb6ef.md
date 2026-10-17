
对于本身，一个点是完全没有意义的：只有当坐标值被映射到轴和/或距离系统时，它才变得有用。在处理 3D 对象时，整个模型被放置在一个名为“模型空间”（`model space`）的坐标系中，范围从负无穷到正无穷。

3D 引擎可以通过它们相互相乘来构建。遗憾的是，矩阵乘法不符合交换律：左侧的操作在右侧的操作之前执行。顺序错误会导致奇异的结果——缩放和旋转始终在平移之前。

将模型引入屏幕分两步完成。首先，执行旋转和缩放操作。你绕着某个轴旋转对象，使其正确地面对摄像头。

在下一步中，通知 `BasicEffect` 传递给它的顶点包含颜色数据：

之后，平移会将对象“推”到它在坐标系中的最终位置。现在是时候逐步查看新版本的 `Draw` 步骤了：

```
protected override void Draw(GameTime gameTime)
{
    GraphicsDevice.Clear(Color.CornflowerBlue);
    BasicEffect cubeEffect = new BasicEffect(GraphicsDevice);
    Matrix cubeRotation = Matrix.CreateRotationY(0.25f);
    Matrix cubeTranslation = Matrix.CreateTranslation(0, 0, -10);
    cubeEffect.World = cubeRotation * cubeTranslation;
    cubeEffect.View = camera.View;
    cubeEffect.Projection = camera.Projection;
```

```
cubeEffect.VerticesEnabled = true;
```

最后，`BasicEffect` 中包含的每个绘制命令都应用到所有顶点：

```
foreach (EffectPass pass in cubeEffect.CurrentTechnique.Passes)
{
    pass.Apply();
    GraphicsDevice.DrawPrimitives(PrimitiveType.TriangleList, 0, 12);
}
base.Draw(gameTime);
```

至此，我们已经准备好运行程序并感受结果了。可以随意修改 `Update` 中的 `Rotation`（旋转）、`Translation`（平移）和 `Scale`（缩放）属性。

首先，创建一个 `BasicEffect` 实例：它是一个调用一组绘制命令的“钩”，旨在替换自定义着色器代码。

# 结论

`BasicEffect` 填充了显示所需的三个矩阵。视图（`View`）和投影（`Projection`）矩阵目前不感兴趣——我们将在以后与着色器编程相关的文章讨论它们。

尽管结果看起来不像我们的游戏，但使用 `DirectX` 或 `OpenGL` 实现这些将会显著增加代码量。退后一步可以发现，大部分用于定义几何对象的代码，将其存储在内容流水线中将使代码更紧凑……这正是我们接下来要做的。

# Springs.io 教程

# 在 Springs.io 上启动可扩展的 Linux 容器

## 了解 cgroups 和 namespaces 如何驱动 Linux 容器，并设置按需付费服务器

![](img/df5857e82a6482b0f2db5a2e61e6012c_43_0.png)

Linux 容器在近年来引起了爆炸性的关注，但所有容器都由 Linux 下的两种底层技术驱动，我们将在本文探索这些技术。在这里，我们将通过一些底层技术将容器与传统的虚拟机进行比较。

# 01 掌握 cgroups 和 namespaces

让我们从什么样的容器开始。它们是轻量级的虚拟服务器形式，与虚拟机相比提供了更好的性能。过去两年中，Linux 内核启用了新一代可扩展容器，这可以让无服务器（`serverless`）方案成为现实。出现了许多用于管理容器的工具，包括 `Docker`、`LXC`、`Incmty`、`Kubernetes` 等。

`Cgroups`（控制组）限制并测量运行在系统的一组进程所使用的资源。`Namespaces`（命名空间）限制了一组进程的可见性。`Cgroups` 和 `namespaces` 允许在隔离的环境中运行一组进程。虽然两者共同工作，但 Linux 内核已为云基础设施带来了一些有趣的应用。`cgroups` 的更新现在对服务器资源使用有了更深入的洞察，允许对进程进行更多隔离，从而提供更好的安全性。

Richard Davis

Springs.io 首席执行兼联合创始人。据此，他是 Spring Technologies PLC & limited 的创始工程师之一，带有视频。

在大多数情况下，系统管理员直接使用 `cgroups` 和 `namespaces` 是没有意义的——容器工具（如 `Docker`、`LXC` 或 `Incmty`）会为你完成这些。但如果你想了解底层原理，而不仅仅是深度使用内核技术的话。尽管如此……

## 资源

Springs.io

springs.io

- 轻量级容器

bit.ly/3hello

- `Cgroups`

bit.ly/h88wccd

![](img/df5857e82a6482b0f2db5a2e61e6012c_43_1.png)

右侧终端：显示 `cgroups` 的进程

![](img/df5857e82a6482b0f2db5a2e61e6012c_44_0.png)

# 01 掌握 cgroups 和 namespaces

在左侧，每个服务器都运行在自己的虚拟命名空间内部。在右侧，`namespaces` 和 `cgroups` 包含了主机操作系统上的所有内容

![](img/df5857e82a6482b0f2db5a2e61e6012c_44_0.png)

命名空间

主机 OS

硬件

控制 `cgroups`

这是一个在 `cgroups` 中运行并限制内存的示例：

```
mkdir -p /sys/fs/cgroup/test
echo 50M > /sys/fs/cgroup/test/memory.limit_in_bytes
echo 50M > /sys/fs/cgroup/test/memory.soft_limit_in_bytes
echo 1000 > /sys/fs/cgroup/test/memory.kmem_in_bytes
echo $$ > /sys/fs/cgroup/test/tasks
```

| PID | USER | COMMAND | STATE | PRIORITY | NI | TIME |
|---|---|---|---|---|---|---|
| 1 | root | systemd | S | 20 | 0 | 0:00 |
| 2 | root | dbus-daemon | S | 20 | 0 | 0:00 |
| 3 | root | kworker/16:1 | S | 20 | 0 | 0:00 |
| 4 | root | kworker/16:2 | S | 20 | 0 | 0:00 |
| 5 | root | kworker/16:3 | S | 20 | 0 | 0:00 |
| 6 | root | kworker/16:4 | S | 20 | 0 | 0:00 |
| 7 | root | kworker/16:5 | S | 20 | 0 | 0:00 |
| 8 | root | kworker/16:6 | S | 20 | 0 | 0:00 |
| 9 | root | kworker/16:7 | S | 20 | 0 | 0:00 |
| 10 | root | kworker/16:8 | S | 20 | 0 | 0:00 |
| 11 | root | kworker/16:9 | S | 20 | 0 | 0:00 |
| ... | ... | ... | ... | ... | ... | ... |

这些行显示了物理 `cgroups` 的状态

前四行设置了 `"test"` `cgroup`——访问物理硬件，限制内存。下一行将我们正在使用的 提示符（以及任何子进程）放入 `"test"` `cgroup` 中。

有很多 `cgroup` 限制可用，它们的完整文档位于：`https://www.cgroups.org/doc/Documentation/cgroups.txt`。

> 传统的资源在 `namespaces` 中运行时会恢复。然而，当守护进程崩溃时，命名空间可能会受到影响，超出传统的控制范围。

# 汇总

如果我们创建两个命名空间，就可以创建一个限制内核内存使用的提示符，并与系统隔离开。通过使用 `cgroups` 进行资源隔离，我们可以限制每个容器可以使用的内容，并实现运行实例与系统的完全隔离。

# 03 控制命名空间

`unshare` 命令允许你隔离命名空间。例如，如果你

```
# unshare --mount /bin/bash
# unshare /dev/null -net
```
