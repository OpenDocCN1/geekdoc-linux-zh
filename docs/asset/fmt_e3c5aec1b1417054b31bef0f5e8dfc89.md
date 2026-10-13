
### CSS 和 HTML

> “使用手机、笔记本电脑或平板电脑等移动设备将使整个项目更加引人注目、流畅且有趣。”

为了使网页看起来体面，你需要设置一个 HTML 文件和一个 CSS 文件。

HTML 代表超文本标记语言，用于创建网页。你的浏览器读取 HTML 文件并将其转换为网页，从而允许将图像和对象嵌入到页面中。层叠样式表，即 CSS，是描述网页外观的代码，即 HTML 内容的呈现方式。

它包含关于元素如何渲染的说明。在这里，它控制开和关选项如何呈现。

### HTML 文件

打开 `Mobile_Lights` 文件夹并创建一个名为 `templates` 的新文件夹。

这个文件夹用于保存包含网站布局结构的 HTML 文件。代码命名了网页标签，并且最重要的是，添加了开和关选项的链接。

从开始菜单打开文本编辑器，或使用 `nano` 创建一个新文件。将下面的 HTML 添加到文件中，然后将该文件保存在 `template` 文件夹中，命名为 `index.html`。记住，这是一个 HTML 文件，必须以文件扩展名 `.html` 结尾。

### 创建新文件夹

安装了 Flask 之后，重启你的树莓派。

在 `/home/pi` 文件夹中创建一个名为 `Mobile_Lights` 的新文件夹。这是你将保存控制插座和灯的 Python 程序以及 CSS 和 HTML 文件的地方。你可以在 LX Terminal 中通过输入 `mkdir Mobile_Lights` 或右键点击窗口并选择“新建文件夹”来创建该文件夹。

```html
<!doctype HTML>
<HTML>
<head>
    <title>Light Controller</title>
    <link rel="stylesheet" href="/static/style.css" />
    <meta name="viewport" content="width=device-width, user-scalable=no" />
</head>
<body>
<div class="on"><a href="/">ON</a> </div>
<div class="off"><a href="/off">OFF</a></div>
</body>
</HTML>
```

### 添加一些样式

CSS 用于创建并将“按钮”样式效果应用于网页。回到 `Mobile_Lights` 文件夹并创建一个名为 `static` 的新文件夹。这是保存 CSS 文件的地方。再创建一个新的文本文件并粘贴下面的代码，该代码定义了网页的样式。你可以从第 20 行开始自定义按钮的颜色。将文件保存为 `static` 文件夹中的 `style.css`。

```css
body {
position: absolute;
margin: 0;
top: 0;
right: 0;
bottom: 0;
left: 0;
font-family: Arial, sans-serif;
font-size: 13px;
text-align: center;
}
div {
display: block;
width: 100%;
height: 50%;
}
div a {
width: 100%;
height: 200%;
display: block;
}
div.on {
background: black;
}
div.on a {
color: white;
}
div.off a {
color: black;
}
a, a:visited {
text-decoration: none;
}
```

### 将所有内容整合在一起

设置过程的最后一部分是编写一个 Python 脚本，将 `index.html` 和 `style.css` 文件与类似于第 7 步中使用的 Energenie 插座控制代码结合起来。

打开 IDLE 并新建一个窗口，添加以下代码并将其保存到 `Mobile_Lights` 文件夹中，命名为 `mobile_lights.py`。第 4 行使用 `route()` 装饰器告诉 `Flask` 使用哪个 HTML 模板来创建网页。第 7 行和第 11 行使用 `app.route('/on/')` 和 `app.route('/off/')` 告诉 `Flask` 当 URL 被点击时触发的函数。在第 15 行使用 `run()` 函数运行我们的应用程序的本地服务器。`__name__ == '__main__'` 确保 Web 服务器仅在脚本直接从 Python 解释器执行时运行，而不用作导入的模块。

```python
from flask import Flask, render_template
from energenie import switch_on, switch_off
app = Flask(__name__)
@app.route('/')
def index():
    return render_template('index.html')
@app.route('/on/')
def on():
    switch_on()
    return render_template('index.html')
@app.route('/off/')
def off():
    switch_off()
    return render_template('index.html')
if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0')
```
