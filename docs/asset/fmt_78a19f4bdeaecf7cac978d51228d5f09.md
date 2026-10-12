
创建一个 Python Web 应用，使用第一人视角控制你的机器人

# 教程

```python
import PyroCore
from cgi import parse_environ, start_response
def application(environ, start_response):
    # 连接到 Pyro
    movement = PyroCore.Proxy('PYRONAME:robotmovement')
    parameters = parse_qs(environ['QUERY_STRING'])
    if 'seconds' in parameters and 'direction' in parameters:
        direction = parameters['direction'][0]
        seconds = int(parameters['seconds'][0])
        # 调用相应的函数
        if direction == 'Stop':
            movement.stop()
        elif direction == 'forwards':
            movement.forward(seconds)
        elif direction == 'backwards':
            movement.backward(seconds)
        elif direction == 'left':
            movement.left(seconds)
        elif direction == 'Right':
            movement.right(seconds)
```

## 步骤 15 树莓派机器人代码列表

![](img/4c82285250803e975d41cda3a51d081f_56_0.png)

```python
status = '200 OK'
else:
    status = '400 Bad Request'
```

```python
response_headers = [['Content-type', 'text/plain'], ['Content-Length', str(len(status))]]
start_response(status, response_headers)
return [status]
```

在 `/home/web/app.py` 中，它也在磁盘上。我们导入了 `Pyro` 核心，以便通过网络调用机器人，还导入了 `cgi` 中的 `parse_qs()` 函数。这允许我们解析在第一步中创建的查询字符串并将其转换为字典。

然后我们注意到我们以 `robotmovement` 注册了 `Pyro` 别名。我们已经连接到它，因此现在我们可以发送命令并检查是否收到了有效响应。如果我们获取了第一个方向和秒数，每个列表中将有一个项目，并调用相应的移动函数。

如果一切顺利，我们返回成功消息，否则返回错误请求消息。用户将看不到延迟，因为我们正在显示视频流且没有冻结。

## 16 更多测试

- 使用 `apache2 restart` 重启 `Apache`

每个错误都会出现，通过在浏览器中输入树莓派的 `IP` 地址来确定并更改服务器。从那里，我们使用按钮和秒数来控制机器人。但机器人在所有运动之后将停止。

我们注意到机器人向前移动 `5` 秒后会停止，在前向移动 `3` 秒时会让机器人后退 `2` 秒并停止。为了解决这个问题，你可以实现一个队列系统。

## 17 如何禁用我们所做的

你可能不希望摄像头通过网络进行广播。如果你只想查看我们做了什么，可以通过在三行的开头添加哈希字符（`#`）来注释掉我们向 `/etc/local` 添加的四行内容。在 `Debian` 上，你可以通过重启来禁用此。

- `apache2` 每次更新后都需要重启，并使用 `sudo service apache2 restart` 启用

- 使用 `/etc/init.d/apache2 start` 停止 `apache`。

## 18 进一步改进

这是你的树莓派 `Web` 界面的一个良好基础，但有很多地方可以改进，使其像：

- 在网页文章上添加添加和调用功能。

- 如前所述，通过 `Apache` 显示视频流。

- 添加身份验证，以便只有拥有用户名和密码的人才能控制机器人。

- 使用 `SSL` 进行安全连接。

- 研究如何处理一个完整周期到单个函数，以及如何用角度关联机器人。

- 如步骤 `15` 提到的，为命令添加队列系统。

# 教程 Qt：一次编写，到处运行

# LinuxDeveloper

![](img/4c82285250803e975d41cda3a51d081f_57_0.png)

![](img/4c82285250803e975d41cda3a51d081f_57_1.png)

# 使用编写，到处运行

`Qt` 是 `C++` 最灵活的跨平台框架，甚至可以创建跨平台 `GUI`。方法如下……

`Eli Hanna` 自 `Palm ITC` 时代以来一直从事 `IT` 行业。作为记者、导师和演讲者，他多次看到了移动市场的各个方面。

在 `C` 的最初开发期间，`GUI` 应用是在一个非用例上开发的：一个具有非图形化哑缩略图的计算机系统。平均开发者觉得自己正在处理引擎代码——如果设计得当，就可以在易于移植的应用程序中使用。

随着时间的推移，操作系统供应商扩展了各种自定义库。这导致移植性水平不断降低，`Windows`、`Linux` 和 `Solaris` 的应用程序，但 `C++` 非亚洲风格代码无法在平台之间共享。

（后来被称为 `Qt`）。框架的开发始于 `1991` 年，该产品成功获得了崇拜的追随者。基于 `Qt` 的 `KDE` 框架的巨大成功引发了对事实实标准的担忧。

`Qt` 的创建者 `Trolltech` 通过引入双重许可方案解决了这个问题。从那时日期起，该框架以两种形式提供：开发者可以购买的（允许他们保留代码）以及也同样提供的 `GPL` 版本。

这催生了挪威的程序员，他们开始开发一种名为 `Qasar` 的产品。

此外，建立了一个法律后门以保护可用性。它负责事实标准。

- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`
- `qt-project.org`

# Qt IDE

`Qt Creator` 为框架的用户提供了一个自定义 `IDE`。`Qt Creator` 在超级模式下运行效果最好。通过在终端中输入命令，启动后，选择选项。

`Qt Creator` 分为多个模块，可以通过帮助菜单激活。任何激活的图标将显示在视图的其余。

```bash
sudo qtcreator
SOFT ASSERT -l "1 -i" in file ..../src/plugins/projectmanager/
```

# 第一步

现在是时候开始编写你的“`Hello World`”应用程序了。选择 `New File or Project` 来创建项目向导。然后，选择 `Application|Qt Application`

选择你想保存应用程序的路径，核心框架和类将被构建。复杂项目需要一些时间来配置参数。

# 新构建过程

当点击左下角的 `Build` 按钮时，框架和类将被构建。复杂项目需要一些时间来配置参数。

基于 `Qt` 的应用程序由操作系统的原生工具编译。该过程由 `make` 控制，`make` 是由一个工具自动生成的。解决方案的项目文件由工具链处理。

# 教程

`Qt`: 一次编写，到处运行

# Linux 开发者

![](img/4c82285250803e975d41cda3a51d081f_59_0.png)

# 跨平台之旅

## 将应用程序迁移到另一个操作系统非常简单
