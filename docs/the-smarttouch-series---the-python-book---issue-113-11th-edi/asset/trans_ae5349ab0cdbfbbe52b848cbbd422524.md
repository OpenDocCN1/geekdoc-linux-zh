
## Web development（Web 开发）

打开 `index.html`。所有在 Flask 模板中执行的代码都包含在 `{% %}` 内。由于这是我们的主页，我们希望据此引导用户。因此，让我们检查是否已经获取了访问令牌（图 01）。在模板的 `if` 和 `else` 之间是标准的 HTML。如果我们想包含一些数据——例如访问令牌——只需在 HTML 中添加 `{{ session["oauth_token"] }}`，它就会在页面上渲染出来。之前，在我们的 /authorised 端点中，我们会显示从 Twitter 接收到的 OAuth 令牌；然而，现在有了模板，我们可以将用户重定向回我们的根 URL，并渲染一个页面来解释我们所取得的进展。

### 06 迷路（然后再次找到方向）

对于每个服务器，某些东西可能会丢失，或者人们可能会迷路。那么，我们如何处理这种情况？与其定义路由，不如定义一个处理迷路情况的处理程序。

```python
@app.errorhandler(404)
def fourOhfour(error):
    return render_template('fourOhfour.html')
```

如果请求某个页面或端点并触发了 404，那么 `fourOhfour` 函数将被触发。在这种情况下，我们将生成一个模板来告知用户，但我们也可以重定向到另一个页面或输出错误消息。

### 07 静态文件

几乎每个网页都使用 JavaScript、CSS 和图片，那么我们把它们放在哪里呢？使用 Flask，我们可以定义一个文件夹用于静态内容。对于 Flask，我们在项目根目录下创建一个 `static` 文件夹，并通过调用 `/static/css/styles.css` 或 `/static/js/core.js` 来访问文件。教程资源中包含一个用于此项目样式的 CSS 文件。

### 08 获取一些推文

现在我们知道如何构建模板了，让我们抓取一些推文来显示。在 `server.py` 中，定义一个新的路由 `get_tweets`，如下所示：

```python
@app.route('/get_tweets/')
@app.route('/get_tweets/<int:count>')
def getTweets(count=0):
```

你会注意到，与其他身份验证端点不同，我们做了两次声明。第一个是标准的路由定义；它将拦截并处理路径 `get_tweets`。第二个让我们定义一个参数，可以作为我们 `getTweets` 函数中的一个值使用。通过在函数声明中包含 `count=0`，我们确保函数执行时始终会有一个默认值；这样，我们在访问值之前就不必检查其是否存在。如果 URL 中包含了一个值，它将覆盖函数中的值。`variable name` 中的字符串决定了变量的名称。如果你希望传递给函数的变量具有特定类型，可以在变量名中包含一个转换器。例如，如果我们想确保 `count` 始终是整数而不是浮点数或字符串，我们会这样定义路由：

```python
@app.route('/get_tweets/<int:count>')
```

### 09 检查我们的会话并构建我们的请求

在我们开始抓取推文之前，我们需要进行一次快速检查，确保我们有必要的凭证，如果没有，则将用户重定向回授权流程。我们可以通过让 Flask 使用重定向响应头来响应请求来实现这一点，如下所示：

```python
if session["oauth_token"] == "" or \
    session["oauth_secret"] == "":
    return redirect(rootURL)
```

假设我们拥有所有需要的东西，我们可以开始构建请求的参数（图 02）。你会注意到，nonce 值与我们之前请求中的不同。我们在 authenticate 和 authorize 请求中的 nonce 值可以是任何唯一标识请求的随机字符排列，但对于所有后续请求，nonce 需要是一个仅使用字符 a-f 的 32 位十六进制字符串。如果我们将以下函数添加到我们的 `helpers.py` 文件中，我们可以为每个请求快速构建一个 nonce。

```python
def nonce(size=32, chars="abcdef" + "0123456789"):
    return "".join(random.choice(chars) 
        for x in range(size))
```

“现在我们知道如何构建模板了，让我们抓取一些推文来显示”

### 10 签署并发送我们的请求

我们已经构建好了参数，所以让我们签署请求，然后将签名添加到参数中（图 03）。

在创建授权头之前，我们需要从 `tweetRequestParams` 字典中移除 `count` 和 `user_id` 值，否则我们刚刚创建的签名对该请求将无效。我们可以使用 `del` 关键字来实现这一点。与我们的令牌请求不同，此请求是一个 GET 请求，因此我们不是将参数包含在请求体中，而是将它们定义为查询参数。

```
?count=tweetRequestParams["count"] 
&user_id=tweetRequestParams["user_id"]
```

### 11 处理 Twitter 的响应

现在我们可以发出请求了，我们应该会从 Twitter 收到 JSON 响应。这是我们之前导入的 `json` 模块的用武之地。通过使用 `json.loads` 函数，我们可以将 JSON 解析为一个字典，我们可以访问该字典并将数据传递给我们的 `tweets.html` 模板。

```python
tweetResponse = json.loads(tweetResponse.read())
return render_template('tweets.html', 
    data=tweetResponse)
```

之前，我们访问会话来获取数据到模板中，这次我们显式地将值传递到我们的模板中。

### 12 显示我们的推文

现在让我们创建模板，与 `index.html` 完全相同，但这次，我们将不使用条件语句，而是创建一个循环来生成我们收到的推文列表。

首先，我们检查是否确实从对 Twitter 的请求中收到了一些数据。如果我们在 `render` 中有一些东西，我们就可以开始处理它，否则我们只输出我们没有收到任何东西。

再一次，我们想要用来生成页面的任何模板逻辑都包含在 `{% %}` 之间。这次我们要创建一个循环；在循环内部，我们可以访问该对象的任何属性并将其打印出来。在这个模板中，我们将为收到的每条推文创建一个 `<li>` 元素，并显示用户的头像和推文文本（图 04）。在我们的模板中，我们可以使用点号表示法（.）或方括号表示法（[ ]）来访问属性。它们的行为大致相同；[ ] 表示法会检查字典或对象定义上的属性，而 . 表示法会查找具有相同名称的项目。如果两者都找不到指定的参数，它们将返回 undefined。如果发生这种情况，模板不会抛出错误；它只会打印一个空字符串。如果你的模板未渲染预期的数据，请记住这一点：你可能只是错误定义了试图访问的属性。与传统 Python 不同，我们需要告诉模板 for 循环和 if/else 语句在哪里结束，所以我们通过 `{% endfor %}` 和 `{% endif %}` 来完成这一点。

### 13 Flask 过滤器

有时，在解析 JSON 时，Python 可能会生成一些在 HTML 中渲染效果不佳的错误字符。你可能会注意到，在 `tweet['text']` 之后有 `|forceescape`。这是一个 Flask 过滤器的例子；它允许我们在渲染之前对输入产生影响——在这种情况下，它为我们转义了值。Flask 附带了许多许多不同的内置过滤器。你的导师建议完整阅读所有潜在选项。

### 14 总结

使用 Flask 进行模板开发基本就是这样了。正如我们所见，构建和部署动态站点非常快速且简单。Flask 是任何希望运行 Web 服务的 Python 开发者的绝佳工具。虽然我们使用 Twitter 来演示 Flask 的强大功能，但这里描述的所有技术都可以用于任何第三方服务或数据库资源。Flask 可以与其他渲染引擎一起工作，例如 Handlebars（它非常出色），但 Jinja2 必须存在才能运行 Flask，并且两个引擎之间可能会发生冲突。由于 Flask 和 Jinja2 之间如此良好的集成，除了非常特定的情况外，使用另一个引擎意义不大。

```python
tweetRequestParams = {
    "oauth_consumer_key": consumer_key,
    "oauth_nonce": helpers.nonce(),
    "oauth_signature_method": "HMAC-SHA1",
    "oauth_timestamp": int(time.time()),
    "oauth_version": "1.0",
    "oauth_token": session["oauth_token"],
    "user_id": session["user_id"],
    "count": str(count)
}
```

```python
tweetRequest = helpers.sign_request(tweetRequestParams, "GET",
"https://api.twitter.com/1.1/statuses/user_timeline.json", consumer_secret,
session["oauth_secret"])

tweetRequestParams["oauth_signature"] = tweetRequest

makeRequest = urllib2.Request("https://api.twitter.com/1.1/statuses/"
"user_timeline.json?count=" + tweetRequestParams["count"] + "&user_id=" 
+ tweetRequestParams["user_id"])

del tweetRequestParams["user_id"], tweetRequestParams["count"]

makeRequest.add_header("Authorization", helpers.create_oauth_
headers(tweetRequestParams))

try:
    httpResponse = urllib2.urlopen(makeRequest)
except urllib2.HTTPError, e:
    return e.read()
```

```python
{% if data %}
<ul id="tweets">
{% for tweet in data %}
<li>
<div class="image">
<img src="{{ tweet['user']['profile_image_url_https'] }}" alt="User Profile Picture">
</div>
<div class="text">
{{ tweet['text']|forceescape }}</div>
</li>
{% endfor %}
</ul>

{% else %}
<p>We didn't get any tweets :()</p>
{% endif %}
```

