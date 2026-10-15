
## 多媒体客户端
客户端连接到多媒体服务器并播放反馈。例如，`XMMS`连接到`Icecast2`。

## 多媒体服务器
负责接受客户端请求并向客户端流多媒体信息。服务器将原始多媒体内容转换为互联网协议 (`IP`) 包，以便跨网络或互联网进行路由。

## 多媒体内容
如果没有内容源，你的多媒体服务器就没什么用了。例如，你的源可以是音乐 `CD`或`DJ`。源可以是固定的也可以是动态的。例如，音乐`CD`是固定源。`Ices2`从固定源读取并将其输入到`Icecast2`。

# 创建音乐源

在创建服务器之前，你必须创建一些播放的内容。本节描述了如何创建一个用于播放的`Ogg Vorbis`文件。我们假设你想从一张商业`CD`创建文件。这种做法是合法的，并且不违反版权法，因为你并没有创建一个在互联网上广播的服务器。相反，你正在创建一个向私有网络广播的服务器。据我们所知，你仍然被允许听自己的`CD`。

### `Ogg Vorbis`音频系统在功能上与`MP3`类似。然而，`Ogg Vorbis`（或简称`Ogg`）是一种开源格式（也称为解码器），与`MP3`不同，它没有任何专利算法或协议。`Ogg`比其他格式具有更高的保真度。`Ogg Vorbis`是两个独立的实体：`Ogg`是一种音频压缩格式，而`Vorbis`是编码。

按照以下步骤创建`Ogg-Vorbis`格式的音乐文件：

- 以任意用户身份登录电脑并插入音频`CD`。
- 点击`GNOME`菜单并选择`Sound & Video: Applications`（声音与视频：应用程序）。`Grip`窗口打开，初始窗口中显示`CD`的曲目。
- 点击你想使用的每个轨目的`Rip`列（位于屏幕右侧）。你选择的每个曲目旁边都会出现复选标记。
- 点击`Config`标签页。打开一个子窗口，显示几个额外的标签页。
- 点击子窗口中的`Encode`标签页。打开另一个子窗口，显示多个配置选项。
- 点击`Encode`下拉菜单并选择`oggenc`。选择`oggenc`告诉`Grip`创建`Ogg`编码的音乐文件。
- 点击窗口顶部的`Rip`（位于`Tracks`标签页旁边）。
- 点击`Rip+Encode`按钮。

`Grip`将音乐从`CD`刻录到电脑文件中。这些文件存储在当前工作目录下名为`rip`的子目录中。`Grip`并不执行`CD`刻录工作；它通过启动`cdparanoia`程序并向其传递选择的参数来运行。曲目被刻录并最初以`Wav`格式保存。`Grip`启动`oggenc`工具并将`Wav`文件转换为`Ogg`格式。

你可以通过在终端模拟器中运行命令 `ogg wav` 来将`Wav`转换为`Ogg`格式。你可以播放`Ogg`编码的文件：`ogg filename.wav`。

你现在有了一个或多个`Ogg-Vorbis`格式的音频文件。你需要安装并配置`Icecast2`和`Ices2`才能广播音乐。

### 安装 `Ices2` 和 `Icecast2`

在本节中，我们告诉你是如何安装应用程序和服务。由于`Ices2`和`Icecast2`都没有提供`RPM`包，因此你必须从头构建。

# 第 19 章：构建流音频服务器

如果你的电脑没有`DVD-ROM`驱动器，你必须使用此书背面的优惠券通过`CD-ROM`获取`Red Hat Linux`。收到`CD-ROM`后，使用它们安装 `libxslt` 和 `automake` 软件包。

现在，你需要从网上下载 `Icecast2` 和 `Ices2` 软件。

- 3. 将你的电脑连接到互联网。

你连接互联网的方法取决于你订阅的服务类型。有关如何将电脑连接互联网的信息，请参阅第 5、第 6 和第 7 章。

- 4. 在 `GNOME Terminal` 窗口中输入此命令：

```
export CVSROOT=:server:anoncvs@xiph.org:/usr/local/cvsroot
```

此命令设置了 `CVS` 完成下载所需的环境变量。环境变量会告知你正在哪个工作环境（在本例中是 `bash`）中工作，以及该去哪里寻找文件和目录等元素。

- 5. 告诉你的 `CVS` 客户端登录到远程 `CVS` 服务器。输入此命令登录远程系统：

```
cvs login
```

- 6. 当提示 `CVS` 服务器密码时，输入 `anoncvs`。

登录成功后，你就可以下载——在 `CVS` 术语中称为 `check out (co)`——软件了。按顺序输入以下命令（在继续下一个之前，等待每个命令完成）。

- 7. 登录后，你可以下载——在 `CVS` 术语中称为 `check out (co)`——软件：

```
cvs co icecast
cvs co ices
cvs co libshout
cvs co ogg
```

你可以看到文件在下载时显示出来，`CVS` 检即完成。

接下来的步骤描述了如何配置、编译和安装你的多媒体服务器：

- 1. 在终端模拟器中运行命令：

```
export LD_LIBRARY_PATH=/lib:/usr/lib:/usr/local/lib
```

需要此环境变量是为了让编译器知道去哪里寻找几个库。

![](img/453364505e32ffec24f7d88ac7824962_304_0.png)

- 2. 配置、编译并安装 `Shoutcast` 库。在终端模拟器中输入此命令：

```
cd libshout
```

- 3. 运行此命令设置编译过程：

```
./autogen.sh
```

- 4. 通过运行 `make` 命令编译并链接软件：

```
make
```

- 5. 安装库：

```
make install
```

- 6. 重复步骤 2–4 创建 `Ogg` 软件。这些命令总结了这些步骤：

```
cd ../ogg
./autogen.sh
make
make install
```

- 7. 重复步骤 2–4 创建 `Ices2` 服务器。这些命令总结了这些步骤：

```
cd ../ices
./autogen.sh
make
make install
```

- 8. 通过编译 `Icecast2` 服务器来完成整个过程。这些命令总结了这些步骤：

```
cd ../icecast
./autogen.sh
make
make install
```

你的 `Ices2` 和 `Icecast2` 服务器现在已准备好进行广播。接下来的部分描述了如何配置这两个服务器。配置完成后，你就可以提供多媒体流了。

# 配置 `Icecast2`

`Ices2` 从静态文件（如 `Ogg Vorbis` 格式的音乐）获取多媒体内容。`Ices2` 将音频流传输到 `Icecast2` 服务器。你可以使用客户端应用程序连接到 `Icecast2` 服务器来听音乐。所有连接都通过 `IP` 网络完成。

`Ices2` 和 `Icecast2` 使用环回 (`127.0.0.1`) 接口进行通信。（环回接口是不使用任何物理设备的内部网络接口。）使用环回接口为测试你的配置提供了一种简单的方法。

`Icecast2` 使用端口 `8000` 与流源通信，使用端口 `8001` 进行管理。

你首先从配置 `Icecast2` 开始：

- 1. 以 `root` 用户身份登录你的 `Red Hat Linux` 电脑。

当你运行 `make install` 命令时，`Icecast2` 配置文件安装在了 `/usr/local/etc` 目录下。现在，你只需要对该文件进行细微修改来设置你的流服务器。

- 2. 点击 `GNOME` 菜单并选择 `Accessories►Text Editor` 以打开 `Gedit` 文本编辑器。

在 `Gedit` 窗口中，选择 `File►Open`。

- 3. 在选择框中输入 `/usr/local/etc/icecast.xml` 并点击 `OK`。

`icecast.xml` 的内容显示在文本编辑器中，如图 19-1 所示。

![](img/453364505e32ffec24f7d88ac7824962_306_0.png)

图 19-1：`icecast.xml` 文件。

- 4. 找到配置文件中定义端口号和绑定地址的部分。移除这些参数的注释。

注释使用字符 `<!--` 来封装配置参数。

- 5. 移除注释后，代码应该像这所示：

```
<!-- You can use these two if you want a single listener
<port>8000</port>
<bind-address>127.0.0.1</bind-address> -->
```

这些参数告诉 `Icecast2` 服务器监听哪个端口号和 `IP` 地址。同时也将主服务器定义为本地机器。

- 6. 找到配置中的 `Master Server` 部分并移除注释。配置应该如下：

```
<master-server>127.0.0.1</master-server>
<master-server-port>8001</master-server-port>
<master-update-interval>20</master-update-interval>
<master-password>hackme</master-password>
```
