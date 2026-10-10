

![](img/8684900d708748f86bb043faa5589f9e_206_0.png)

## 图 9.4 在 Swift 对象存储界面中查看你的容器

既然容器是一组对象的集合，让我们把这个容器命名为“zoo”（动物园），并往里放入一堆以动物为主题的文件。同时勾选标有“public”（公共）的复选框，以便该容器可以通过 http 在 OpenStack 外部访问。我们将在本章后续部分中使用这个功能，在网页上显示一个对象。

一旦你点击 **Create**（创建），你就会返回到对象存储页面，在那里你可以点击你容器的名称，查看有关它的详细信息，如图 9.4 所示。

现在我们实际上想向你的容器添加对象。请记住，对象只是一个文件，因此你可以上传各种各样的东西作为对象。作为一个简单的测试，我们将从一个简单的文本文件开始。在你运行网络浏览器以访问 Horizon 仪表盘的同一台机器上，打开一个终端并创建一个简单的文本文件：

```
$ echo “Black and white striped African equid” > zebra.txt
```

点击红色垃圾桶图标左侧带有向上箭头的图标以上传此对象。如图 9.5 所示的“Upload File To: zoo”（上传文件到：zoo）屏幕将弹出，允许你从文件系统中选择文件并将其上传。点击 **Upload File**（上传文件）以完成此操作。

你可以多次执行此操作，上传几种不同类型的文件。混合添加一个图像文件，以便在本章后续部分中将其用于在网站上包含图像的实际示例。由于 Swift 的标志是一只鸟，我们上传了 eagle.jpg。在图 9.6 中可以看到 zoo 容器中文件列表。

要了解有关特定对象（如大小和内容类型）的更多信息，请查找对象右侧“Download”（下载）旁边的向下箭头并点击。选择标有 **View Details**（查看详情）的选项。

![](img/8684900d708748f86bb043faa5589f9e_207_0.png)

图 9.5 创建容器屏幕

![](img/8684900d708748f86bb043faa5589f9e_207_1.png)

图 9.6 带有 zoo 容器及其内容的对象存储屏幕

![](img/8684900d708748f86bb043faa5589f9e_208_0.png)

图 9.7 Swift 中对象的详细信息

如图 9.7 所示，这将打开一个屏幕，提供有关该对象的基本信息。

既然你已经成功创建了一个容器并添加了一个对象，你可以继续学习使用 OpenStack 客户端在命令行上创建容器和对象的过程，或者跳过本章稍后的“使用对象”部分，查看如何在实际示例中使用你创建的对象。

### 创建容器和对象：OpenStack 客户端

仪表盘是与 OpenStack 交互的便捷方式，但 OpenStack 客户端和特定语言的 API 使你可以有效地为这些操作编写脚本，并在不包含 Horizon 仪表盘的部署环境中执行这些操作。当你在独立部署环境中运行 Swift（不包含许多其他 OpenStack 组件）时，这尤其有价值。为了简单起见，请登录控制器节点以完成这些操作。

#### 提示

与前面的章节一样，本章中 OpenStack 命令的输出已整理并按章节分类，可通过在线 GitHub 仓库复制并更易于阅读：https://github.com/DeploymentsBook/scripts-and-configs。

我们首先要做的是使用测试用户创建一个容器，我们的对象将存储在其中。测试用户也将用于向该容器添加对象：

```
$ source /etc/openrc.test
$ openstack container create aquarium
```

| 账户 | 容器 | x-trans-id |
| :--- | :--- | :--- |
| KEY_33a65b0402b047c097d21864b72c06be | aquarium | tx8d138c08f743482a089735-00571c050f |

现在我们将创建几个简单的文本文件对象，添加到容器中：

```
$ echo "An eight-legged cephalopod mollusk" > octopus.txt
$ echo "Common member of the sub-grouping of the mackerel family" > tuna.txt
```

现在将这些对象添加到名为 aquarium 的容器中：

```
$ openstack object create aquarium octopus.txt
```

| 对象 | 容器 | etag |
| :--- | :--- | :--- |
| octopus.txt | aquarium | 228654098af0e1e8d22c5801c5466d |

```
$ openstack object create aquarium tuna.txt
```

| 对象 | 容器 | etag |
| :--- | :--- | :--- |
| tuna.txt | aquarium | 1bef3811c46128a7b755d4846f1f0439de |

要在容器中显示这些对象，请使用 `list` 命令：

```
$ openstack object list aquarium
```

| 名称 |
| :--- |
| octopus.txt |
| tuna.txt |

**提示**

使用 `--long` 标志配合 openstack object 的 `list` 命令，以获取容器中文件的基本详细信息。

你还可以显示容器本身的详细信息，包括其使用的存储空间和对象数量：

```
$ openstack container show aquarium
```

| 字段 | 值 |
| :--- | :--- |
| account | KEY_33a65b0402b047c097d21864b72c06be |
| bytes_used | 92 |
| container | aquarium |
| object_count | 2 |

假设你还向容器中添加了一张动物图片，Swift 将使用 object show 命令显示该对象的属性：

```
$ openstack object show aquarium dolphin.jpg
```

| 字段 | 值 |
| :--- | :--- |
| account | KEY_33a65b0402b047c097d21864b72c06be |
| container | aquarium |
| content-length | 172154 |
| content-type | image/jpeg |
| etag | 3b67e3cdf756bc0e3adf05820398251bb |
| last-modified | Sat, 23 Apr 2016 23:43:15 GMT |
| object | dolphin.jpg |
| properties | Orig-Filename='dolphin.jpg' |

如你所见，这将显示文件类型（image/jpeg）、大小、修改日期以及更多内容。

### 使用对象

无论你是使用 Horizon 仪表盘还是 OSC 创建的对象，你现在都希望实际使用该对象。第一步是确保你的容器是公共的，然后你需要找出其中特定文件的地址。在仪表盘中，导航到对象存储，容器以查看你之前创建的 zoo 容器。点击 zoo，并确认 **Public Access**（公共访问）旁边有一个复选标记，如图 9.8 所示。

现在点击 **Public Access** 链接，这应该带你访问一个类似于以下地址的 URL：

```
http://10.190.0.8:8080/v1/KEY_33a65b0402b047c097d21864b72c06be/zoo
```

10.190.0.8 是运行 Swift 代理服务器守护进程的服务器地址。在我们的场景中，由于仪表盘和 Swift（具体而言，Swift 代理服务器）都在控制器上运行，因此这与你的仪表盘地址相同。

![](img/8684900d708748f86bb043faa5589f9e_210_0.png)

图 9.8 启用公共访问的容器

现在，将你希望引用的对象名称附加到该地址之后，以便在浏览器中加载你的对象。例如，我上传了 *eagle.jpg* 图像，因此我将使用以下地址访问该对象：

```
http://10.190.0.8:8080/v1/KEY_33a65b0402b047c097d21864b72c0bbe/zoo/eagle.jpg
```

如果你更愿意使用 OpenStack 客户端（OSC）来处理此事，你可以使用 `container show` 命令查看是否设置了 `read-acl`：

```
$ source /etc/openrc.test  
$ openstack container show zoo
```

| 字段 | 值 |
| :--- | :--- |
| account | KEY_33a65b0402b047c097d21864b72c0bbe |
| bytes_used | 92268 |
| container | zoo |
| object_count | 4 |
| read_acl | .r:*, .rl:lists |

如果输出不包含 `read_acl` 行，你可以使用以下 Swift 客户端命令进行设置：

```
$ swift post -r .r:*,.rl:lists zoo
```

如果你再次运行 show 命令，应该会出现该行。

现在你需要构造访问对象的 URL。其格式如下，将 IP 地址替换为你环境中正确的地址，并将“account”（账户）和“container”（容器）替换为 show 命令中的值。“object_name”（对象名称）将是你希望引用的对象（如 *eagle.jpg*）：

```
http://10.190.0.8:8080/v1/account/container/object_name
```

结果看起来像这样：

```
http://10.190.0.8:8080/v1/KEY_33a65b0402b047c097d21864b72c0bbe/zoo/eagle.jpg
```

这可以加载到浏览器中，你应该能看到该图像，但它也可以包含在网页中，正如我们接下来要演示的那样。

### 网页中的对象

为了进行更贴近实际的演示，我们创建了一个包含简单 HTML 文件的仓库，你可以在 Ubuntu 实例上使用。使用你首选的方法，遵循第 6 章“私有计算云”中概述的说明，启动一个 Ubuntu 14.04 计算节点。你可能还希望为该实例添加一个浮动 IP 地址以改善访问。

一旦该节点正在运行，你可以在控制器上或你的 Ubuntu 实例的 SSH 密钥所在处运行以下命令。将 10.190.0.8 替换为你启动的实例的正确地址：

```
$ git clone https://github.com/DeploymentsBook/http-files.git  
$ scp -r http-files/swift/ ubuntu@10.190.0.8:
```

