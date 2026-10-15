
-- 初始化 Snort --

正在初始化（全局）

日志目录`/log`

`scap`配置为被动模式。

正在从 `"eth0"`获取网络流量

正在实时解码...

```

```

-- 初始化完成 --

- `Snort +`:

  版本 2.9.70 (Build 549)

  作者 Mark White 和 Snort 团队：`http://www.snort.org/team`

  版权 (C) 2014 Cisco 及其关联公司。保留所有权利。

  版权 (C) 1999 Source, Inc., 等。

  使用 `libcap` 版本 1.6.2

  创建于 2014-04-04

  使用 `ZLIB` 版本: 1.2

```

```

开始处理数据包 (`pid:1955`)

警告: 策略 8 未配置处理器。

警告: 策略 8 未配置处理器。

警告: 策略 8 未配置处理器。

```

离开 `Snort` 后，数据包日志模式将实时识别数据包流量

![](img/a54b3b473771472dd2321ddda1014be1_42_0.png)

```

$ snort -dev -1 -log

```

你可以从命令中看到，不需要指定详细模式或 `-e` 开关。在二进制模式下，数据包会被完整记录，而不仅仅是部分内容。如果你需要启用网络入侵检测，可以使用以下命令：

```

$ snort -dev -1 -home $HOME_NET -etc/snort/

snort.conf

```

请注意，`Snort` 是你的文件名，而 `HOME_NET` 是配置文件中定义的变量值。`snort.conf` 文件中的规则部分将应用于每个数据包，并对每个数据包做出是否需要采取行动的判断。默认动是 `alert`（警告）。另一个规则文件会在调用命令之前读取 `snort.conf` 的条目，其应用程序行为是先处理 `Pass`（通过）规则，然后是 `Alert`（告警）规则，如该命令所示：

```

$ snort -h 192.168.1.0/24 -1 /log -etc/snort/

snort.conf

```

另一个重要点是我们需要理解 `Snort` 配置。`Snort` 提供了多种选项来显示输出和检测到的信息。许多网络安全管理员需要监控和调查由 `Snort` 生成的信息。为了做到这一点，`Snort` 必须以支持多输出插件并允许安全管理员使用各种工具的格式输出数据。我们来快速查看一些 `snort` 配置：

- `Alert syslog`（警告系统日志）：基于 UNIX 的系统使用 `syslogset` 来合并检测到的消息。`Snort` 生成的信息可以用不同的方式呈现在 `syslog` 中。如果你在 `snort` 配置中使用 `syslog`，格式如下所示

需要注意的是，如果你正在使用 `IDS`（入侵检测系统），为了速度考虑，你不应该在命令行中使用 `-u` 开关。当作为网络入侵检测系统时，`Snort` 提供了实时检测能力。

输出 `syslog: <facility> <Priority>`
示例：`output snort:LOG_AUTH_LOG_ALERT`

```

$ snort -A fast -etc/snort/snort.conf -lib

```

在某些情况下，我们对 `Snort` 的性能感兴趣。在这种场景下，你可以使用 `-A` 和 `-fast` 选项。输出将以 `tcpdump` 格式记录，这将提供极少的告警。你可以使用以下命令实现此目的：

- `tcpdump`：将数据包记录到 `tcpdump` 文件。多种应用程序可以读取这种格式。
- `MySQL`：日志记录要求运行 `Snort` 的系统存在数据库支持，形式为 `MySQL` 软件和库。

另外请注意，`Snort` 按照特定顺序将其规则应用于数据包。默认顺序是先应用 `Alert`，然后是规则，最后是 `Log`（日志）。`Snort` 提供了 `-o` 开关来更改默认规则

最后说明，既然你已经知道了如何使用 `Snort`，最好在防火墙后面运行它，因为这增加了一层保护并使快照更容易获取。

`www.luxuser.com` 43

![](img/a54b3b473771472dd2321ddda1014be1_43_0.png)

可以添加阴影来轻松赋予你的球体 3D 质

# 不要慌

在写作此时，`MonoGame` 的内容流水线相当不错——在许多情况下，编译项目将会失败。别担心，这可能意味着你什么都没做。如果发生这种情况，请启动一个 Windows 项目和一个新的内容项目。`Pipeline` 工具将生成一组 `.xnb` 文件，这些文件会被复制到你的 `MonoGame` 项目的 `/Content` 文件夹中。`Image()`;

通过缓存部分数学计算可以节省资源，乘法是最耗能的计算操作之一。对于我们的简单示例，基本方法就足够了。

现在是时候加载 `LoadContent` 了。下面的方法生成了一个总共十个随机位置的球体：

![](img/a54b3b473771472dd2321ddda1014be1_44_0.png)

之后，可以在 `LoadContent` 中加载内容。`MonoGame` 的内容处理器使用 `Microsoft`，因此扩展在编译期间会被删除——我们的代码段在没有的情况下也能工作

```c

protected void LoadContent ()

```

```

spriteBatch = new SpriteBatch(GraphicsDevice);

model = Content.Load<Model>(

```

```

myModel = new Model(one, Vector3(3,0,0));

myMatrix = new Matrix.Identity;

for (int i = 0; i < 10; i++) {

myBalls = new ModelClass(ball, 0.5f,Random.Next(-10,10),Random.Next(-10,10));

}

```

运行上述代码会让 `MonoGame` 将坐标加载到内存中；在教程的最后部分，`Model` 类没有为变换和其他几何信息留出空间。这通过创建一个自定义模型类来解决，如下所示

`XNA` 没有提供一种方便的方法在指定范围内返回随机数的 `RNG`（随机数生成器）。我们通过 -10 到 10 的范围改变三个球体的位置。

```csharp

public class ModelClass

{

    public Vector3 position;

    public float rotation;

    public float scale;

    public ModelClass(Model model, float scale, float x, float y)

    {

        // ... 实现

    }

}

```

```csharp

public void Draw(SpriteBatch spriteBatch)

{

    foreach (ModelClass ball in myBalls)

    {

        // ... 绘制逻辑

    }

}

```

![](img/a54b3b473771472dd2321ddda1014be1_46_0.png)

```cpp

if (myPosition.Z < -10 || myPosition.Z > 10) {

  dz = -1;

  myPosition=new Vector3(myPosition.X,myPosition.Y,myPosition.Z);

}

```

如果发生碰撞，违规对象将通过乘以 -1 来反转。最后一次移动是为了防止对象以意外的加速度附在边界上。

各个模型之间的碰撞检测是一个更复杂的过程。尽管我们的对象相对简单，但在每个平面上进行相交计算会过度消耗几何计算。

这可以通过包围对象轻松地解决。这些几何体可能会使用球体或八面体——建立在每个元素周围。然后，可以通过比较两个元素的边界来执行基本的碰撞检查，只有在 `ClassModel` 的情况下才部署更复杂的算法，需要以下修改：

```c

public void rotateMatrix() {

  myMatrix = Matrix.CreateScale(new Vector3(scaleFactor)) * Matrix.CreateTranslation(myPosition);

}

```

```cpp

mySphere = myModel.Meshes[0];

foreach(Mesh m in myModel.Meshes) {

  myBoundingSphere = BoundingSphere;

  CreateMerged(myBoundingSphere,myBoundingSphere.Transform(myMatrix));

}

```
