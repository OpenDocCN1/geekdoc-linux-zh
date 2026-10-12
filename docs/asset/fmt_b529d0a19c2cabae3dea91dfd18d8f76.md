
### HTTP POST 请求

客户端向 `Web` 服务器发送信息的基本单元是 `HTTP POST` 请求；通常，它们由某些表单生成，并配置用于传输任何类型的数据。`HTML` `form` 中的 `enctype` 字段指定了将应用于数据上的编码类型。通常，编码会执行字符替换（例如将空格替换为字符），我们使用 `multipart/form-data` 是因为我们不希望以任何方式修改数据。

![](img/06332f0e1d4d0e5b78061a5103897f51_55_1.png)

## `LU-Tube`

面向 `Linux` 用户的视频共享平台

### 上传视频

选择文件：`nil`

标题

上传

### 我们的视频

- 每日提示

```html
<span style="position:fixed; font-size: large; color:yellow">在海滩边</span></span>
```

- 每日提示

上述注入攻击是常见的（参见第 57 页方框）且危险的破坏服务器安全的手段。

注入攻击通过 `Go` 的 `HTML` 模板库得到了修复，该库处理了特殊字符。

我们将结果变量存储在一个表单中，以便可以使用。当被调用时，`Go` 将将数据从 `HTTP` 请求传输到程序的内存中。该值将一直存储，直到达到 `RAM` 最大字节数，然后它会将数据存储为临时文件。

多个返回值使得这特别有用。我们应该处理以下情况：

```go
title := request.FormFile("title")
```

```go
if err != nil {
    return err
}
```

如果有错误，我们会立即处理它：

我们需要为视频生成一个唯一的 `ID`。我们利用 `os` 包中的 `TempDir` 函数来实现这一点。该函数用于创建一个会被删除的临时目录。`TempDir` 始终确保目录名称与现有目录冲突。

```go
video, err := request.FormFile("file")
defer video.Close()
```

```go
videodir, err := os.TempDir("video", "")
defer os.RemoveAll(videodir)
```

我们现在可以从视频请求的调用者处下载数据。首先，我们将视频上传到文件：

`TempDir` 在文件系统上创建一个新目录，并返回一个指向该目录路径的字符串，第二个参数是设置目录用户 `ID` 的可选参数。如果有错误，我们必须处理它。

`Form` 的参数是 `HTML` 表单中字段的。它返回文件和一个错误值（带有文件头信息），

下一步是保存视频文件。这可能很复杂，但目前编写一个简单的函数就足够了。我们已经写好了这个函数，所以我们可以使用 `uploadVideo` 完成编写工作。

> 我们需要为视频生成一个唯一的 `ID`，利用 `os` 包中的 `TempDir` 函数。

```go
err := saveVideo(video, id, title, videoFile)
```

我们忽略了它。你应该在这里添加此代码来处理错误。

在这种情况下，立即处理错误可能更好。为 `getErrorMessage` 函数添加一个缓存通道（`cache channel`），这将允许用户显示某些“文件上传错误”的消息。

下一行是一个 `defer` 语句，这是我们尚未遇到过的特殊 `Go` 结构。`defer` 意味着“在函数结束时执行此命令”。这是一种让代码运行的非常有用的方法，无需跳转到函数底部编写它。如果函数有

它应该将用户重定向到他们新视频所在的页面，以便他们立即开始享受。如果还没有返回错误，我们将使用 `nil` 通道向用户信号发生了某些事情

```go
http.Redirect(writer, request, "/video/" + id, )
```

## 防御注入攻击

`Go` 非常擅长保护我们免受注入攻击。当恶意用户尝试向输入字段中插入代码以便绕过安全限制并访问您的系统时。

在图 7 中，我们看到一次良性注入攻击尝试：有人决定为首页标题样式，因此他们在标题字段中添加了 `HTML` 样式。他们没有输入粗体字符，而是在 `<body>` 标签处使用了 `<span style="position:fixed; font-size:large; color:yellow">Richard</span>` 使标题像图像一样固定在页面顶部。在 `HTML` 页面上，我们可能预期这种攻击是成功的。他们的 `HTML` 代码被正确打印，因为像 `<` 和 `>` 这样的特殊字符已被替换为适当的 `HTML` 实体，例如 `&lt;` 和 `&gt;`。

我们使用 `HTML` 模板。如果我们查看数据，即用于上传视频的文件，我们看到它包含了 `HTML` 代码。然而，播放器库足够聪明，将其转换为安全格式并直接渲染，而不允许用户通过 `HTML` 注入流游戏。

```go
http.StatusOK()
return nil
```

将数据拷贝到文件系统

最后一步是编写 `saveVideo` 函数。该函数将接收一个视频结构体和一个作为流（`stream`）的文件：

```go
func saveVideo(video *Video, file io.Reader) (err error) {
}
```

我们需要在文件顶部添加 `import`。

让我们编写函数体。首先我们应该在文件系统中创建一个文件，以便拷贝数据：

```go
videoFile, err := os.Create("/videos/" + video.ID + ".mp4")
defer videoFile.Close()
return err
```

由于我们使用了 `os.Create` 创建文件，我们需要在文件的导入语句中添加 `os`。不要忘记返回错误值。然后我们可以使用 `io.Copy` 将视频数据拷贝到

![](img/06332f0e1d4d0e5b78061a5103897f51_56_0.png)

## `LU-Tube`

面向 `Linux` 用户的视频共享网站

### 上传视频

| | |

### 我们的视频

- 每日提示

我们将从用户处接收的数据写入创建的文件：

```go
err := io.Copy(videoFile, file)
```

现在，我们需要将视频保存到数据。然后我们使用 `os.Create` 创建文件：

```go
videoData, err := os.Create(videoDir + "/data.txt")
defer videoData.Close()
```

最后一步是将标题写入文件，我们可以使用 `WriteString` 方法实现：

```go
err := videoData.WriteString(title)
```

在此处，我们返回错误值：

```go
return err
```

`localhost:8080`

# 概览

- `Purism` 的操作系统：`Pure OS p60`

什么是 `Pure OS`？`Purism` 移动操作系统代表了什么？

- 支持的操作系统：`Plasma Mobile p62`

`Purism Mobile` 提供 `KDE` 移动体验

- 支持的操作系统：`Ubuntu Touch p64`

`Ubuntu` 在 `UUBports` 上运行于 `Librem 5`

- 额外功能：`Android` 版 `Linux p66`

无需 `root` 即可在 `Android` 手机上运行 `Linux`

![](img/06332f0e1d4d0e5b78061a5103897f51_58_0.png)

`Purism` 是一家成立于 2014 年总部位于旧金山的计算机（以及很快将是移动设备）制造商。`Purism` 符合开源自由软件制造的理念，旨在让个人能够轻松地在他们信任并感到安全的设备之间进行选择。它曾筹集了超过 100 万美元（在众筹阶段），以将其专注于安全和隐私的“`Librem`”电脑带市场。除了拥有 20 多名员工外，它还拥有一个全球社区，该社区将隐私、安全和自由视为默认配置。其方法与苹果、谷歌或微软等大公司采用的方法背道而驰，这些公司忽视了产品和隐私安全的重要性。保护数字权利是一项长期挑战。`Purism` 的创始人兼首席执行官 `Juan Andres Luna` 将其描述为“提供一种方便的替代计算环境，以颠覆科技巨头的通用数字惯例”。

## `Purism` 提供了一种方便的替代环境，以颠覆科技巨头的通用数字惯例

高端规格（尽管由于大型制造商的机器，这些规格经常被更新为“最新”和“最强”）。再次强调，隐私和安全是至关重要的，制造和采购决策始终将其作为首要任务。得益于 `PureOS`，他们允许你在机器上运行版本为 0.8 的“`Prometheus`”（目前正处于测试阶段），它基于 `Debian`，并将最佳的隐私保护软件与 `Gnome 3` 以及 `Wayland` 结合，以实现快速、流畅和优的电源管理。套件包含了 `Firefox ESR` 以及热门类别中的其他应用程序，所有应用都经过了完全验证。

目前正在开发中的 `Librem 11` 是一款 11 英寸的“二合一”笔记本电脑，为公司的操作系统提供了一个多功能平台；这是自配备 5 英寸屏幕的 `Librem 5` 以来最有野心的项目。
