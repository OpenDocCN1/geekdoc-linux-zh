
回顾一下几十年前的技术……你在寻找什么？原版 `Game Boy`？`Apple II`？软盘驱动器？`Sinclair`？录音带？这些东西有什么共同点？它们都有非常小的存储空间。当然，这是相对的说法——请结合当今每平方厘米的存储容量来考量。很久以前，填满 `1.44Mb` 只有那些最 prolific（多产/高产）的计算机用户才能做到。但随着音乐、视频、照片和大型游戏充斥着你的存储空间，将所有内容保存在一个设备上已变得近乎不可能。还要毫不费力地与朋友和家人分享所有这些内容？算了！超过 `20Mb`？这就是 `Dropbox` 发挥作用的地方。在本教程中，我们将编写一个脚本，自动将文件与 `Dropbox` 服务器同步，从而避免文件丢失的烦恼。

#### 01 设置你的 Dropbox 应用

为了向 `Dropbox` 上传文件和文件夹，我们需要创建一个具有读写权限的应用程序。如果你访问 `www.dropbox.com/developers/apps`，你会看到一个列表，显示以某种形式访问你的 `Dropbox` 账户的应用程序。

点击窗口右上角的“创建应用（Create app）”按钮，你会看到两个选项：创建用于“Drop-ins”的应用，或创建使用 `Dropbox API` 的应用。我们将使用核心数据 API，因此选择第二个选项，然后选择随后出现的“文件和DataSource（Files and Datasources）”选项。在设置完成前的最后一个是“你的应用程序可以限制在自己的文件夹内吗？”虽然这不是必须的，但在以编程方式处理事务时，在应用程序和宝贵数据之间保持一定程度的隔离总是很有用的。简而言之，在这种情况下，选择“是”。输入应用名称，你就准备好了。接下来你会看到该应用的设置视图。记下你的应用密钥（`app key`）和秘密（`secret`），因为稍后你会用到它们。在开始之前，前往你应用程序的根文件夹并创建两个新文件夹——一个命名为“Files”，另一个命名为“Folders”。这些稍后会很有用。

然后这将输出一个代码——访问令牌（`access token`）。回到你的命令行，会有一个提示符等待你粘贴刚才收到的代码。有了这个代码，`Dropbox` 库将请求一个 `OAuth` 令牌，该令牌将贯穿整个会话使用。如果一切顺利，你应该现在能在终端中看到你的账户详情被打印出来。

#### 02 使用 Python 连接 Dropbox

现在我们在 `Dropbox` 方面已经设置好了应用，我们需要让 `Python` 与之通信。下载 `Python Dropbox SDK` 并解压，然后运行：

```bash
$ python setup.py install
```

你的 `Python` 环境应该已准备好开始通信。创建一个新文件夹，名字随意，在该文件夹内创建一个名为 `watcher.py` 的新文件。打开你新建的文件，然后插入 **图 01**。`Dropbox` 有几种不同的方法允许你认证他们的服务。在本教程中，我们将使用所谓的“无流程（no flow）”认证方法。这种方法允许我们在不处理任何重定向的情况下认证应用，但它需要少量的复制粘贴操作。如果你运行上述脚本，它会打印出一个 `URL` 供你访问。前往该链接并点击“认证（authenticate）”按钮，

#### 03 稍后保存我们的认证令牌

现在我们可以访问 `Dropbox` 账户了，但我们不想每次运行脚本时都要经过认证流程，所以让我们将其保存到一个文件以供将来使用。在我们的 `get_token()` 函数中 `client` 变量之前，添加以下内容：

```python
print access_token
storeToken = open('token.txt', 'w')
storeToken.write(access_token)
storeToken.close()
client = dropbox.client.DropboxClient(access_token)
```

现在，当我们将来认证我们的应用时，我们的令牌将被保存。让我们编写一个检查其存在的逻辑。创建一个名为 `run()` 的新函数：

在 `run` 内部，我们将检查是否存在名为 `token.txt` 的文件。如果存在，我们将读取其内容，尝试用它创建一个 `Dropbox` 会话，如果因任何原因失败（令牌过期/格式错误），则请求一个新的。我们可以用以下代码实现：

```python
def run():
    haveTokenFile = os.path.isfile('token.txt')
    if haveTokenFile is True:
        f = open('token.txt', 'r')
        createClient(f.read())
    else:
        get_token()

if __name__ == '__main__':
    run()
```

![](img/daaca9116bc2b1db669c224de81abc7c_42_0.png)

上图：一旦新应用程序的 `API` 请求被授权，我们就可以开始使用 `Python SDK`

你会注意到我们尝试调用一个新函数 `createClient`。让我们现在编写它。（图 02）

在这里，我们的代码将尝试访问 `Dropbox`，如果失败则在再次尝试连接前请求一个新令牌。我们需要修改 `get_token` 函数以反映这一变化。如果你替换...

```python
# 旧
client = dropbox.client.DropboxClient('access_token')
# 新
createClient('access_token')
```

...这两个函数现在将协同工作，以找到并连接到 `Dropbox`。如果没有抛出错误，我们就准备好开始查看我们要上传哪个文件了——但我们的脚本如何知道我们要存储什么？为此，我们将创建一个 `JSON` 文件和一些解析逻辑来确定需要备份哪些文件和文件夹。

#### 04 向我们的脚本传递参数

我们不希望在不变化的情况下不断向 `Dropbox` 上传文件，所以现在我们将组装一些代码来跟踪我们系统中正在同步到 `Dropbox` 的文件和文件夹。在我们的 `run()` 函数中，我们将添加一些代码，让我们可以根据传递给脚本的参数——或者称之为“模式（modes）”——来改变脚本的行为。首先要添加的是检查传递给脚本的参数数量。如果少于两个，则只传递了脚本的文件名。这对我们帮助不大：让我们添加一个要求，必须传递单词 `run` 才能执行目前的脚本。（图 03） 并添加对我们刚写的语句的编辑。（图 04）

现在我们有了一种向脚本传递要存储项目的方法——但为什么我们要区分文件和文件夹？为了上传一个文件夹，我们需要将该文件夹中的所有文件连同定义的路径一起传递给 `Dropbox`。如果我们尝试上传到一个尚未存在于我们的 `Dropbox` 账户中的文件夹，它会收到一个错误。通过分别跟踪文件夹和文件，我们将能够在尝试上传任何内容之前检查它们的存在性和状态。

**图 01**

```python
import sys, os, time, dropbox, json
app_key = 'YOUR_APP_KEY'
app_secret = 'YOUR_APP_SECRET'
client = None

def get_token():
    global client
    flow = dropbox.client.DropboxOAuth2FlowNoRedirect(app_key, app_secret)
    authorize_url = flow.start()
    print("Open the following in your browser:")
    print(authorize_url)
    token = raw_input("", and then enter your authorization code here: ")
    access_token, user_id = flow.finish(token)
    print access_token
    client = dropbox.client.DropboxClient(access_token)
    print client.account_info()

if __name__ == '__main__':
    get_token()
```

**图 02**

```python
def createClient(token):
    global client
    try:
        client = dropbox.client.DropboxClient(token)
        load_list_of_watched_files_and_folders()
    except dropbox.rest.ErrorResponse, e:
        print("Error accessing Dropbox. Likely because of an expired token.")
        get_token()
```

**图 03**
