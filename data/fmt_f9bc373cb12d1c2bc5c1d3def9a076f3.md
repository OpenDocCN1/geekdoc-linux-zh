
## 06 创建我们的第一个路由

为了验证用户，我们需要创建一个用户可以访问并触发路由的端点。在 `Flask` 中这个过程非常简单：使用路由装饰器（`@app.route`）来触发函数或操作。我们想要创建的端点是身份验证后的重定向，由用户执行。注意，虽然我们不需要函数名称与端点名称相同，但 `Flask` 可以提供静态文件或使用渲染模板，为了简单起见，我们在第一个路由的末尾返回一个简单的文本响应来显示我们的进度。

```python
import urllib, urllib2, collections, hmac, binascii, time, random
from hashlib import sha1
from flask import redirect, session, Flask

# Twitter API 变量
consumer_key = 'Y9nMRDu355Xev'
consumer_secret = '8svrrB4klvHjWlZCU9WbtopzdXvZgJ6bb'

app = Flask(__name__)

@app.route('/authenticate')
def authenticate():
    session['secret'] = '...'

    request_params = {
        'callback': 'https://api.twitter.com/auth/',
        'consumer_key': consumer_key,
        'nonce': str(random.randint(1, 999999999)),
        'signature_method': 'HMAC-SHA1',
        'timestamp': str(int(time.time())),
        'version': '1.0'
    }
    return sign_request(request_params, "https://api.twitter.com/")
```

## 07 创建一个 flask session

为了维护变量并为用户设置特定值，我们将值存储在 `Flask` session 中。`session` 是使用 `cookie` 存储值来实现此最安全的方法，但由于我们使用了一层加密来保证用户凭据的安全，它的行为就像字典，因此我们可以使用字典拥有的所有方法。例如，如果我们需要存储身份验证令牌，可以使用 `session.class`。我们需要确保在对 `session` 进行任何调用之前，我们设置了 `secret key` 以避免错误。我们选择在 `app()` 中设置 `secret key`，这样它会在服务器执行之前被设置。对于大多数情况，这就是我们需要的。

```python
@app.route('/callback')
def callback():
    request = urllib2.request(request)
    token = request.args.get('oauth_token')
    if token:
        session['oauth_token'] = token
        return redirect('https://api.twitter.com/authorize?oauth_token=' + token)
    else:
        return HTTPError('404')
```

## 08 准备授权我们的应用

现在我们开始演示如何向 `Twitter` 提交数据。`OAuth` 协议要求每个请求都使用 `SHA1` 哈希值进行签名，以便 `Twitter` 能够验证收到的数据的完整性。

```python
def verifyRequestParameters(request):
    verify_params = {
        'consumer_key': consumer_key,
        'nonce': str(random.randint(1, 999999999)),
        'timestamp': str(int(time.time())),
        'version': '1.0',
        'oauth_token': session('oauth_token')
    }
    signature = sign_request(verify_params, "POST", "https://api.twitter.com/")
    request.add_header("Authorization", "oauth=" + signature)
```

![](img/5ff17f60221cc9f68eff9bca50f06afb_44_0.png)

# 教程

# 处理 Twitter 的注销 OAuth 流程

## LinuxDeveloper

为了正确对请求签名，我们需要将参数按字母顺序排序，对其进行 `URL` 编码，拼接然后每次对它们进行签名。这是一个 `OAuth` 编码问题。由于我们几乎对每个请求都要执行此操作，我们将编写一个方便的函数来完成所有这些工作：`sign()`

> `Flask` 非常适合这个项目：定义路由和处理器的参数就像制作蛋糕一样

![](img/5ff17f60221cc9f68eff9bca50f06afb_45_0.png)

## 09 创建我们的签名

首先，我们需要使用请求的基础 `URL`，这可以通过 `urllib.quote()` 实现。接下来，我们为传递给函数的参数创建一个有序字典，根据键值按字母顺序排序。由于每个请求都必须使用正文中的所有参数进行签名，因此正确排序它们非常重要。接下来，我们创建一个变量体来存储我们将将用于请求的方法字符串，并将其附加其中。然后，我们通过对字典的键值对进行拼接和 `URL` 编码来构建体，从而获得我们的签名。然后我们检查体是否为空；如果不为空，我们在下一步中将在体签名中添加一个 `&`。

## 10 签名密钥

现在我们需要为我们的签名创建一个签名密钥。正如我们所说，我们将使用我们的 `consumer_secret` + `oauth_secret` 与

## 11 获取密钥

使用 `HMAC` 库对密钥进行哈希。我们将使用我们的签名字符串（请求体的内容）。`SHA1` 哈希函数处理签名。

## 12 获取请求令牌

我们不能仅仅请求令牌来访问数据。首先，我们需要获取请求令牌，然后对其进行交换。这是我们在后端自己完成的。在此期间，如果我们想尝试任何事情，我们需要提交给 `Twitter` 的签名值。`call_auth()` 在我们在第一个身份令牌重定向之前无法起作用。我们想要将其指向 `/authenticated`。

## 13 构建头部

当我们签名请求时，我们需要正确编码并格式化我们的授权头部。`sign_request()` 和 `auth_headers()` 之间的主要区别是我们使用了请求体。如果使用了错误的头部，请求将被拒绝。

## 14 创建请求令牌

一旦获取了头部，我们就回到 `HTTP` 请求并调用 `oauth()` 方法等待响应。如果一切顺利，我们将在响应中收到一个包含第一个身份验证令牌的字符串。然后我们需要单独对该字符串进行解析，使用 `getParameters()` 函数，它将解析字符串并返回一个我们可以访问的字典。我们将使用这些令牌用于后续的请求。

## 15 减少请求

现在我们有了第一个身份验证令牌，我们可以减少我们的授权屏幕以让他们获取数据。除此之外，我们可以使用 `flash` 重定向到我们的视图。此请求是少数可以使用 `OAuth` 参数发送令牌的请求之一

# 关于 oauth_nonce 的一点介绍

`OAuth` 头部和签名过程中的大多数值都是可选的。然而，`oauth_nonce` 是一个随机生成的值 - 字母数字型，但由于没有定义的约定，可以使用整数用于此目的。它是为了让 `Twitter` 检查是否重复发送了相同的请求。

![](img/5ff17f60221cc9f68eff9bca50f06afb_46_0.png)

# 教程

# 使用 Django 构建博客

## LinuxDeveloper

| `Django` 测试 `Web` 服务器正在运行 | 使用 `Django Admin` 创建一篇新的博客文章 | 首次执行 `'python manage.py syncdb'` 命令 | 显示 `Django` 用于创建测试数据库的 `SQL` 命令 |

![](img/5ff17f60221cc9f68eff9bca50f06afb_47_0.png)

## 使用 django 构建博客

## 顾问

Mihalis Tsoukalos 是一位 `UNIX` 系统管理员，同时也精通编程、数据库和数学。他自 1999 年以来就一直使用 `Linux` 操作系统。

## 学习如何通过简单的步骤编程并发布 Django 照片博客站点
