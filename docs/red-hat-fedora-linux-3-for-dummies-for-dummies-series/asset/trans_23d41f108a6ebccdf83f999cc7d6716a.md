

这些步骤有助于你为 Fedora Core 计算机做好准备，以便开始构建多服务器：

- 1. 以任意用户身份登录你的计算机。
- 2. 打开 Mozilla 浏览器，访问 www.icecast.org，然后点击页面顶部的“Download”（下载）链接。

现在你需要从互联网上下载 icecast2 和 ices2 软件。

- 3. 点击 `icecast-2.0.2.tar.gz` 链接。

此时会弹出一个标题为“Opening icecast-2.0.2.tar.gz”的对话框。

- 4. 点击“Save it to disk”（保存到磁盘）选项，然后点击“OK”（确定）按钮。

此时会弹出一个标题为“Enter name of file to save to...”（输入要保存的文件名……）的对话框。

- 5. 点击“Save”（保存）按钮。

文件将被下载到你的计算机中。

- 6. 回到浏览器中，向下滚动页面并点击 `libshout-2.0.tar.gz` 链接。

“Enter name of file to save to...”（输入要保存的文件名……）对话框将打开。

- 7. 点击“Save”（保存）按钮，`libshout` 归档文件将被下载到你的计算机中。

- 8. 再次回到 www.icecast.org 网页，点击页面右上角的“Ices”链接。

Ices 下载页面将打开。现在该下载 ices2 源代码了。

- 9. 点击 `ices-2.0.0.tar.gz` 链接。

“Enter name of file to save to...”（输入要保存的文件名……）对话框将打开。

- 10. 点击“Save”（保存）按钮。

ices2 文件将下载到你的当前目录中。

请注意，在这一节中，我们打破了仅从 RPM 包安装预编译软件这一未明说的规则。虽然 Icecast2 提供有 RPM 格式，但 ices2 并没有。我们本可以使用 Icecast2 软件包，但它需要一个难以找到的库（在多个程序间共享的软件）。因此，从头编译 Icecast2 和 Ices2 反而更简单。（了解我们这类技术宅是怎么度过周六夜晚的，也挺有趣的！）

在安装 Icecast2 和 Ices2 之前，我们必须先安装 libshout 库：

- 1. 点击 GNOME 菜单并选择 System Tools:: Terminal（系统工具:: 终端），打开一个终端窗口。

这些说明假设你是在主目录下进行操作。

- 2. **切换为 root 用户：**

```
su
```

请注意我们没有使用 `su -` 命令。使用短横线（-）会告知替代用户（su）命令采用新用户的环境并切换到新用户的家目录。这包括切换到用户家目录，会使这个过程变得复杂。

- 3. **解包 libshout 归档文件并切换到新的 libshout 目录。**

```
tar xzf libshout*
cd libshout-2.0
```

- 4. **运行以下命令以设置编译过程：**

```
./configure
```

- 5. **通过运行 make 命令来编译和链接软件：**

```
make
```

- 6. **安装软件：**

```
make install
```

libshout 库被安装到 `/usr/local/lib`。接下来的说明展示了如何配置、编译和安装 Ices2 多服务器。

- 1. **返回上一级到你的主目录：**

```
cd ..
```

- 2. **解包 Ices2 归档文件：**

```
tar xzf ices-2*
```

星号匹配主版本号——2 之后的任何字符。我们在这里使用它，以防 Ices2 的版本号发生了变化。

- 3. **切换到你在步骤 2 中通过 tar 命令创建的 Ices2 目录：**

```
cd ices-2*
```

- 4. **运行以下命令以设置编译过程：**

```
./configure
```

- 5. **通过运行 make 命令来编译和链接软件：**

```
make
```

- 6. **安装软件：**

```
make install
```

Ices2 软件被安装在 `/usr/local` 目录中。

- 7. 将示例配置文件复制到其工作位置，并向上移动一级：

```
cp conf/ices*.xml /usr/local/etc
cd ..
```

接下来，使用以下方法配置、编译和安装 icecast2。

- 1. 解包 icecast2 归档文件：

```
tar xzf icecast*
```

- 2. 切换到新创建的 icecast2 目录：

```
cd icecast*
```

- 3. 配置 icecast2 以供编译：

```
./configure
```

- 4. 编译源代码：

```
make
```

- 5. 安装代码：

```
make install
```

icecast2 软件被安装在 `/usr/local` 目录中。

- 6. 将示例配置文件复制到其工作位置：

```
cp conf/icecast2dist /usr/local/etc/icecast.conf
```

现在，你的 ices2 和 icecast2 服务器已准备就绪，可以正式运行。下一节将描述如何配置这两个系统。配置完成后，你就可以提供多媒体流了。

## 配置 Icecast2

Ices2 从静态文件（例如格式为 Ogg/Vorbis 的音乐）中获取多媒体内容。然后，Ices2 将音频流提供给 icecast2 服务器。你可以使用客户端应用程序连接到 icecast2 服务器来收听音乐。所有这些连接都是通过 IP 网络进行的。

Ices2 和 icecast2 使用回环（127.0.0.1）接口进行通信。（*回环接口是一个内部网络接口，不使用任何物理设备。*）使用回环接口提供了一种测试配置的简单方法。

> Icecast2 使用端口 8000 与其流源进行通信，使用端口 8001 进行管理。

你首先配置 Icecast2：

- 1. 创建 icecast 用户。

```
useradd -m -d /var/log/icecast icecast
```

此用户将用于运行 icecast 服务器，但由于我们没有设置密码，因此它不会作为登录账户使用。

- 2. 切换到 /usr/local/etc 目录。

- 3. 打开 Icecast2 配置文件，如下所示：

```
gedit icecast.xml
```

现在，你需要对配置文件进行一些微小的修改，以设置你的简单流媒体服务器。

- 4. 找到定义端口号和绑定地址（127.0.0.1）的配置文件部分。移除这些参数的注释。

注释将这些字符字符串 `<!--` 和 `-->` 封装在配置参数周围。

- 5. 移除注释后，代码应如下所示：

```xml
<!-- You can use these two if you only want a single listener -->
<port>8000</port>
<bind-address>127.0.0.1</bind-address>
```

这些参数告诉 Icecast2 服务器要监听的端口号和 IP 地址。它们还将主服务器定义为同一台机器。

- 6. 找到配置中的 Master Server（主服务器）部分并移除注释。配置应如下所示：

```xml
<master-server>127.0.0.1</master-server>
<master-server-port>8001</master-server-port>
<master-update-interval>120</master-update-interval>
<master-password>hackme</master-password>
```

- 7. 找到 `<logdir>` 参数并将其更改为以下内容：

```xml
<logdir>/var/log/icecast/</logdir>
```

这是保存有关运行中的 Icecast2 服务器所有信息（在日志中）的位置。有关 Icecast2 问题的信息也放置在那里。

- 8. 找到 `<security>` 部分并将用户和组更改为 icecast：

```
<security>
  <chroot>0</chroot>
  <!--
    <changeowner>
      <user>nobody</user>
      <group>nogroup</group>
    </changeowner>
  -->
</security>
```

以 nobody 用户运行服务器可以降低安全风险——入侵你的 Icecast2 服务器不会给黑客提供超级用户权限。

- 9. 移除 `<changeowner>` 参数之前和 `</changeowner>` 参数之后的注释：

```
<security>
  <chroot>0</chroot>

  <changeowner>
    <user>icecast</user>
    <group>icecast</group>
  </changeowner>

</security>
```

移除注释可使 `<user>` 和 `<group>` 指令生效，并强制 Icecast2 以用户和组 nobody 运行。如果你不移除注释，Icecast2 将以启动它的进程的用户和组身份运行。由于你以 root 身份登录，Icecast2 将以 root 用户身份运行。

![](img/41feae212f5c6612ff709354891f7b39_302_0.png)

以任何 root 权限运行任何服务都可能危及计算机的安全。

- 10. 点击“Save”（保存）按钮保存你的更改。
- 11. 通过选择 File → Quit（文件 → 退出）退出 Gedit。

你刚刚启动了多服务器，但还没有传输任何内容。现在处于静默状态。由于你不想触犯 FCC（联邦通信委员会），下一节将描述如何配置并启动 Ices2 服务器，以便向 Icecast2 服务器提供内容。

## 配置 Ices2

配置 Ices2 类似于配置 Icecast2。按照以下步骤配置 Ices2，然后向 Icecast2 提供音频流：

