
为此，我们将教你如何使用 `gst-streamer` 软件将视频直接从树莓派流到你的浏览器。现在我们已经就绪，并将转换上一期指南中的运动代码，以便它可以从我们的小型 Web 应用中执行，然后用 Python 编写它。这就像树莓派一样简单！

# 资源

- 一个树莓派机器人（请参 `LUD 132` 指南）

- 树莓派摄像头模块及 `WiFi` 连接

## 使用第一人称视角通过网页控制树莓派机器人

创建一个使用 `mayGI` 控制机器人的 Python 应用。

# 教程

## 01 连接摄像头

摄像头应连接到树莓派，以太网口的蓝色一侧朝后，带有引脚的一侧朝向 SD 卡。抬起连接器，将排线尽可能推到底，然后按下连接器以固定它。

## 02 启用摄像头

使用你的用户名和密码 `raspberry` 登录树莓派系统。你使用的版本可能不支持树莓派。运行 `apt-get update` 以确保你是最新版本。一旦完成，运行 `raspi-config` 并选择启用摄像头的选项。你需要重启以使更改生效。

## 03 安装 mpeg-streamer

我们将使用一个尚未为树莓派打包的 `mpeg-streamer` 实验版本。因此，我们需要通过 `Subversion` 从索引中编译它。运行 `apt-get update`，然后我们需要下载源代码。`mpeg-streamer` 需要所有的依赖项。你可以通过以下命令安装它们：

```
sudo apt-get install libjpeg8-dev cmake
```

## 04 编译 mpeg-streamer

如下所示：

```bash
git clone https://github.com/linuxamaser/mpeg-streamer
cd mpeg-streamer/src
experimental
make
sudo make install
```

```bash
export STREAM_PATH=/home/pi/mpeg-streamer/mpeg-streamer-experimental
export LD_LIBRARY_PATH=$STREAM_PATH:$LD_LIBRARY_PATH
$STREAM_PATH/streamer -i "input-raspiprc -d 200" -o "output-x26ink"
```

```bash
exit 0
```

![](img/4c82285250803e975d41cda3a51d081f_54_0.png)

## 05 开始测试

在我们运行 `mpeg-streamer` 之前，我们需要导出路径以便加载器可以找到模块。我们将导出为 `STREAM_PATH` 以获得一个友好的名字，但路径不在 `LD_LIBRARY_PATH` 模块中。我们通过以下变量找到它：

```bash
export STREAM_PATH=/home/pi/mpeg-streamer/mpeg-streamer-experimental
export LD_LIBRARY_PATH=$STREAM_PATH:$LD_LIBRARY_PATH
```

现在通过以下方式启动 `mpeg-streamer`：

```bash
$STREAM_PATH/streamer -i "input-raspiprc -d 200" -o "output-x26ink" -w $number=1 /
```

... `$number` 是客户端的数量。你现在可以通过 IP 地址 (`http://<ip-address>:8080/test`) 查看视频。

## 06 启动时启动 mpeg-streamer

通过将 `rc.local` 复制到 `/etc/rc.local`，然后编辑 `/etc/rc.local` 添加我们的脚本，在最后一行之前添加 `exit 0`。重启树莓派以确保其工作。你的 `rc.local` 文件应该像这样：

## 步骤 06

## 07 安装 Apache 和模块

我们将使用 `Apache` 作为我们的 Web 服务器，`WSGI` 作为从 Web 服务器导出 Python 并调用函数的方法以访问 `GPIO`。`mpeg-streamer` 实际上是以 `root` 身份运行的，可以通过界面轻松修复。或者，你可以安装包：

```bash
sudo apt-get install apache2 apache2-mod-wsgi
```

我们还需要设置代理服务器来连接我们的模块。编辑 `/etc/apache2/mods-available/proxy.conf` 并启用它。然后我们需要启动代理脚本：

```bash
sudo /etc/init.d/mpeg-streamer-start
```

## 08 配置 WSGI

我们想使用 `WSGI` 控制我们的机器人。我们的导出脚本将以 `robotweb` 调用命令。编辑 `/etc/apache2/sites-available/00-default` 以启用 `WSGI`。在 `VirtualHost` 节中添加以下行：

```
WSGIProcess robotweb group=robotweb multiprocess=1 threads=2
```

## 09 WSGI Hello World

使用 `WSGI` 控制我们的机器人。在你喜欢的编辑器中打开 `/home/robotweb/app.py` 并将代码添加到顶部。每当我们想要命令机器人时，通过传递摄像头流来启动 `WSGI` 工作。

![](img/4c82285250803e975d41cda3a51d081f_54_1.png)

![](51cda3a51d81f_54_2.png)

```python
def application(environ, start_response):
    status = '200 OK'
    output = 'Hello World!'
    response_headers = [('Content-type', 'text/plain'),
                        ('Content-Length', str(len(output)))]
    start_response(status, response_headers)
    return []
```

## 步骤 09

```bash
wget 'http://maxcdn.github.io/jquery.form.js'
```

```bash
wget 'http://ajax.googleapis.com/ajax/libs/jquery/1.7/jquery.js'
```

## 11 启动时启动运动服务器

正如我们讨论的那样，我们想通过将其添加到 `/etc/rc.local` 在启动时启动运动服务器。我们使用了以下行：

```bash
/home/robotweb/movement_server.py
```

## 12

`Bootstrap` 需要使用 `Twitter` 的 `Bootstrap` 框架作为我们的 Web 界面。该目录位于 `/var/www/`，我们可以通过删除默认 `Apache` 页面开始，然后下载并提取 `bootstrap` 文件：

```bash
wget 'https://github.com/bootstrap/bootstrap/download/v3.0.0/bootstrap-3.zip'
```

```bash
unzip bootstrap-3.zip
mv dist . /
rm -rf bootstrap-3.zip
```

## 13 创建运动代码

下一个代码基于我们上一个机器人项目的运动和超声波传感器。然而，运动传感器（超声波部分）有很大不同，因此我们将其正确添加到代码中。我们重写了 `movement.py`（可以在磁盘上找到）。你还需要使用 `chmod +x` 使文件变为可执行。我们想使用 `Pyro` 类更改机器人的速度。

`movement` 类需要继承 `PyroObject` 以便可以远程调用。我们需要从 `movement` 类函数的部分集成基类。那里有一个普通方法。对于每个方向，我们使用 `GPIO` 端口在相应的引脚上输出高或低一段时间，然后调用移动电机速度的函数。

最后，我们通过向 `PyroServer` 注册并启动请求循环来设置 `Pyro` 服务器，它只需等待 `Pyro` 客户端的请求并执行相应的函数。

## 14

主体有一个容器，显示了我们的世界，以及一个表单，允许我们向机器人发送一个方向和持续的时间。当点击按钮时，网页即可工作，秒文本框的值会被发送到动作脚本，以及所点击按钮的方向。

注意树莓派的 `IP` 是硬编码的，因为我们需要在端口 `8000` 上访问流。你可以使用 `DNS` 地址或通过 `Apache` 端口反向代理视频流。

## 15 在我们的 Web 应用中调用运动代码

我们的应用程序非常简单。它只需要接收一个方向和一个持续时间。编辑代码页面以替换我们创建的 `Hello World` 代码。

## 16 它接收一个移动的方向和一个持续的时间

# 通过网页控制你的树莓派机器人
