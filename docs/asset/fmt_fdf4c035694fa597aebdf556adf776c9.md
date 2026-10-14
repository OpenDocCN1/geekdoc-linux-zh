
![](img/287427b4a3b7d7792fc1ca7834fce232_152_2.png)

## 18 分类

首先使用 `parent_id` 定义来过滤正确的文章，返回 `response_category = Post.objects.filter(category__slug=slug)` 和 `render_to('blog/category.html', {'category': response_category})`。再次使用新模板我们将

## 19 分类 URL

我们将使用 `urls.py` 中的 URL 来处理文章页，而不是在链接中使用 ID：`url(r'blog/%<slug:slug>/', 'blog.categories')`

## 20 分类模板

使用这个类似的示例作为分类模板：`{% for post in category_posts %}<a href="/blog/post/{{post.id}}">{{post.title}}</a> - {{post.date|date:"M d, Y"}}{% endfor %}{{% if not category_posts %}未找到文章。% endif %}{{% if Category: {{category.name}}{% endif %}`

## 23 RSS 链接

我们需要为馈链接项目，以便项目可以链接到正确的文章。我们必须获取文章工作的绝对 URL：`post.link = "http://127.0.0.1:8000/blog/{{post.id}}/"` 返回 `link`

![](img/287427b4a3b7d7792fc1ca7834fce232_152_3.png)

## 24 RSS URL

最后一步是将 feed 添加到 `urls.py`：`url(r'blog/feed/', 'blog.feed')`。现在你的博客已经可以正常运行了。通过一些微调和完善，你就可以将其上线并尽情博客了！

> 最后，让我们通过更改将分类引导到相关页面

《Python Book》153

## 在 Pi 上使用 Python

156 使用你的 Pi 进行运动追踪
在 Pi 程序中加入运动检测

158 在 Pi 上处理 OpenGL
使用 Python 生成 3D 图像

160 将 Ras Pi 转换为定格动画工作室
制作一部定格动画电影

164 从树莓派发送短信
结合简单的 Python 代码和 Twilio

166 使用 Pi 进行人脸识别
使用 Pi 识别目标人物

168 学习 Sense Hat
编写一个版本的“剪刀石头石头布、蜥蜴、史派克”

172 掌握 Sense Hat 技能
结合简单的 Python 代码和 Twilio

![](img/287427b4a3b7d7792fc1ca7834fce232_153_0.png)

![](img/287427b4a3b7d7792fc1ca7834fce232_154_0.png)

158

168

```javascript
var z = "script"
```

《Python 之书》155

## 在 Pi 上使用 Python

### 激活你的 Pi 运动追踪

## 学习使用树莓派、摄像头和一些 Python 代码来追踪图像

到此时，你已经知道可以使用摄像头和树莓派来实现某些功能。这让你能够在程序中包含图像捕获，但一旦你的代码运行起来，你还可以做更多事情。在本章中，我们将查看如何向你的 Python 程序中添加运动检测。

这种高级图像处理起来非常困难，因此我们将在他人的努力工作的基础上进行定义。具体来说，我们将使用出色的 OpenCV 包。它在不断改进，并随着更新添加了更多功能。

你还需要安装与摄像头和 OpenCV 通信所需的 Python 包。可以通过以下方式安装包：

```bash
sudo apt-get install python3-picamer opencv-python own
```

这将自动安装所有依赖项。在这个项目中，你将使用用于树莓派的 PICamera，但如果你想使用 USB 摄像头，我们指出其他选项。要与摄像头通信，你需要使用 `picamera` 模块中的 `PICamera` 类。

```python
from picamera import PICamera
from picamera import tuple
camera = PICamera()
camera.resolution = tuple((640,480))
frame = camera.capture()
frame = np.array(frame, dtype=np.uint8)
```

你已经准备好了摄像头以及一个用于存储捕获图像的内存缓冲区。有几种不同的方法可以进行运动追踪。简单的方法之一是尝试观察何时发生了变化。有一个名为 `numpy` 的 Python 模块提供了几个在此过程中非常有用的基础图像处理函数。我们将为此使用它：

```bash
sudo pip install numpy
```

为了查看图像，我们需要看到背景是什么样的。我们可以拍摄一系列图像并查看这些图像的平均值来获取背景的概念。当新图像与背景不同时，我们就知道发生了变化。这种变化在灰度图中最为明显。为了找到这一点，我们将图像转换为灰度，然后消除任何高对比度区域。我们只需运行一个持续循环，从帧中捕获图像然后处理捕获的帧。此图像没有数据封装，所以你有责任记住你正在处理的内容。循环中的下一步是检查我们是否有平均图像，如果没有则初始化它。在第一次循环时，代码将执行：

```python
if avg is None:
    avg = gray.copy().astype('float')
    raise.truncate('count')
    continue
```

现在我们有了平均图像，可以将任何后续捕获的图像添加到加权平均值中。我们需要找到当前图像与加权平均值之间的差异。

```python
cv2.weighted(gray, avg, 0.5)
diff = cv2.absdiff(gray, avg)
```

通过使用这种差异，我们将能够检测运动，而不会因为光线变化产生误报。现在我们有了与平均值的差异，该如何处理？我们如何判断差异足够足够？我们需要设置一个阈值，表示图像与平均值之间的“巨大”差异。如果我们对此差异图像进行阈值处理，就可以继续寻找轮廓以识别与平均背景不同的物体功能。

```python
imgThreshold = cv2.threshold(diff, 25, 255, cv2.THRESH_BINARY)[1]
contours, _ = cv2.findContours(imgThreshold, ...)
```

在这里我们使用 OpenCV 函数来处理图像处理步骤。我们注意到我们实际上是在处理原始的数组表示。

《Python 之书》

## 在 Pi 上使用 Python

### 摄像头如何？

在主文章，我们一直在使用插入树莓派 USB 接口的 Pi。但如果你手头没有现成的设备，可以在家里找找，树莓派有一个摄像头模块，但帧率没有使用 Arduino 模块时那么好。关键是让 OpenCV 图像分析函数符合预期。你也可以通过文件名使用设备，同时也用于连接到树莓派的摄像头。假设你已经连接了摄像头，你可以连接到它：

确保你已连接了摄像头，你可以连接到它：

如果我们想通过画边界框来检测移动物体，我们使用这个：

```python
for c in contours:
  if cv2.contourArea(c) > 500:
    (x,y,w,h) = cv2.boundingRect(c)
    cv2.rectangle(frame,(x,y),(x+w,y+h),(0,255,0),2)
```

如果我们想实时监控结果，我们将使用：

```python
cv2.imshow("Motion detected", frame)
```

# 在树莓派上使用 Python

## 在树莓派上处理 OpenGL

树莓派包含一个基础 GPU。学习如何使用它在板卡上生成 2D 图形。

我们在本栏目中过的许多示例都包含在控制台上运行的程序。我们将介绍如何在你的 Python 代码中包含图形。板卡上的硬件非常强大，但为了充分利用这些设备，请注意您需要将实际显示器连接到树莓派。如果没有显示器，可以通过 SSH 配合 X11 转发连接到树莓派。通过在桌面电脑上运行 X11 服务，您可以在本地机器上进行显示。要从 Python 访问 OpenGL，你需要安装正确的包：

在微软世界中，它本质上是针对非微软软件的 DirectX。所有功能都封装在 C 语言编写的库中，而 `pyopengl` 提供了一组 Python 包装器以便方便使用。

在 Python 中使用 OpenGL 的第一步是导入窗口模块。创建后，有几类函数可用。它们被归类在 GLU 和 GLUT 子模块下。
