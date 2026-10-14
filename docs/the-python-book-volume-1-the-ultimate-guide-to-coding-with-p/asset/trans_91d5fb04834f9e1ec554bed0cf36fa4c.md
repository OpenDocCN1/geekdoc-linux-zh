

# 将你的 APK 发布到 Play 商店

了解如何为发布版 APK 进行数字签名并上传到你选择的应用程序商店

1 构建并签名发布版 APK
首先我们必须先创建一个个人数字密钥，然后使用它为 APK 的特殊发布版本进行数字签名。运行以下命令，并按照它们随后给出的说明操作。

## 创建你的个人数字密钥
你可以自行选择
密钥库名称、别名和密码。
$ keytool -genkey -v -keystore test-release-key.keystore
-alias test-alias -keyalg RSA
-keysize 2048 -validity 10000

## 以发布模式编译你的应用
$ buildozer android release

## 使用你的新密钥签名 APK
$ jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1
-keystore ./test-release-key.keystore
-bin/KivyBreakout-0.1-release-unsigned.apk test-alias

## 对齐 APK zip 文件
$ ~/buildozer/android/platform/android-sdk/tools/zipalign -v 4
-bin/KivyBreakout-0.1-release-unsigned.apk
-bin/KivyBreakout-0.1-release.apk

2 注册成为 Google Play 开发者
访问 https://play.google.com/apps/publish/signup，并按照说明操作。你需要支付一次性 25 美元的费用，但之后你可以上传任意数量的应用。

3 将你的应用上传到商店
点击“添加新应用”以将你的应用提交到商店，包括上传你的 APK 并添加描述文本。准备就绪后，只需点击发布，你的应用应该在几个小时内上线！

```
self.parent.do_layout()
self.parent.destroy_blocks(self)

class Game(FloatLayout):
    def destroy_blocks(self, ball):
        for i, block in enumerate(self.blocks):
            if ball.collide_widget(block):
                y_overlap = (
                    ball.top - block.y if ball.velocity[1] > 0
                    else block.top - ball.y) / block.size_hint_y
                x_overlap = (
                    ball.right - block.x if ball.velocity[0] > 0
                    else block.right - ball.x) / block.size_hint_x
                if x_overlap < y_overlap:
                    ball.velocity[0] *= -1
                else:
                    ball.velocity[1] *= -1
                self.remove_widget(block)
                self.blocks.pop(i)
                if len(self.blocks) == 0:
                    self.win()
        return  # Only remove at most 1 block per frame
Fig. 10
```

```
title = Kivy Breakout  # Displayed in your app drawer
package.name = breakout  # Just a unique identifying string.
                          # along with the package.domain
fullscreen = 0  # This will mean the navbar is not covered
log_level = 2  # Not vital, but this will print a lot more debug
               # information and may be useful if something
               # goes wrong
Fig. 11
```

![](img/3b256f430f51c98f1315671f6e4eec19_60_0.png)

你的游戏应该可以在任何现代 Android 设备上运行……你甚至可以构建一个发布版本并发布到应用商店！

# 使用 Python 制作 Web 应用

Python 提供了快速简便的方式来构建应用程序，包括 Web 应用。继续阅读，了解如何使用它来构建功能完整的 Web 应用

Python 以其简洁性和功能而闻名。此时它已经如此先进，以至于你可以用 Python 做任何事情，而征服网络就是其中之一。当你使用 Python 进行 Web 开发时，你可以访问庞大的模块目录和社区支持——充分利用它们。

Python 的 Web 开发可以有多种不同方式，从使用老式的 CGI 模块到利用完善的 Web 框架。后者是使用 Python 构建 Web 应用最流行的方法，因为它允许你在不必担心所有底层实现细节的情况下构建应用。有许多 Web 框架可用于 Python，例如 Django、TurboGears 和 Web2Py。对于本教程，我们将使用我们目前的首选方案 Django。

# 01 创建 Django 项目 杂志刊号跟踪器

django-admin.py 文件用于创建新的 Django 项目。让我们为我们的刊号跟踪器项目创建一个……

在 Django 中，项目代表站点及其设置。另一方面，应用程序代表站点的特定功能，如博客或标签。这种方法的优点是你的 Django 应用程序具有可移植性，并且可以用很少的精力集成到其他 Django 站点。

```
$ django-admin.py startproject ludissuetracker
```

将创建一个项目目录。这也将作为随 Django 提供的开发 Web 服务器的根目录。在项目目录下你会找到以下项目……

manage.py：用于与你的项目协作的 Python 脚本。

ludissuetracker：你的项目的 Python 包（包含 __init__.py 文件的目录）。该包包含你的项目的设置和配置数据。

# 02 配置 Django 项目设置

在开始处理应用程序之前，让我们根据我们的需求配置 Django 项目。

按如下方式编辑 ludissuetracker/settings.py（仅显示需要修改的部分）：

数据库设置：我们将使用 SQLite3 作为数据库系统。

注意：红色文字表示新代码或更新的代码。

```
'default': {
    'ENGINE': 'django.db.backends.sqlite3',
    'NAME': 'ludsite.db',
```

# 路径设置

Django 需要目录设置的绝对路径。但我们希望能够传入相对目录引用。为了做到这一点，我们将添加一个辅助 Python 函数。在 settings.py 文件顶部插入以下代码：

```
import os
def getabspath(*):
    return os.path.join(os.path.abspath(os.path.dirname(__file__)), * )
```

现在你可以更新路径选项：

```
TEMPLATE_DIRS = (
    getabspath('templates')
)
MEDIA_ROOT = getabspath('media')
```

# 资源

Python 2.7：
https://www.python.org/download/releases/2.7/

Django 版本 1.4：
https://www.djangoproject.com/

