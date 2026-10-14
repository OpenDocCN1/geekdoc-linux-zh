

## 使用 Python 创建

```
try:
    session['verified'] == True
except KeyError:
    session['verified'] = ''

try:
    session['loggedin'] == True
except KeyError:
    session['loggedin'] = ''

try:
    session['user'] == True
except KeyError:
    session['user'] = ''
```

## 06 登录

双因素认证的第一步是使用传统的用户名/电子邮件和密码登录。访问你的数据库并使用以下查询创建一个新用户：

```
INSERT INTO users (username, password, phonenumber) VALUES ( 'USERNAME', 'PASSWORD', '+44YOURUSERSPHONENUMBER' )
```

出于本教程的目的，密码是明文的——但我们恳请你，在生产环境中实现密码时，务必对其进行哈希处理。尽管如此，现在我们仍将使用明文密码。我们的 login.html 模板有一个表单，它将 POST 到 check-user，在这里我们将检查凭据的有效性，然后在需要时触发验证。因此我们将使用 MySQLDB 模块从数据库获取详细信息。

为了查询数据库，我们需要创建一个游标来执行我们的 MySQL 语句。我们通过 `cur = db.cursor()` 来实现：

```
@app.route('/check-user', methods=['POST'])
def checkUser():
    #session.clear()
    if request.method == 'POST':
        #print request.form['username']
        cur = db.cursor()
        cur.execute("SELECT * FROM users WHERE username = %s" , (request.form['username'],))
```

```
result = cur.fetchone()
returnedPassword = result[2]
returnedPhoneNumber = result[3]
```

我们可以使用 `cur.execute()` 构建 SQL 语句。注意 `%s`；它将被下一个变量中传递的值替换。我们使用 `cur.fetchone()` 执行语句，它将获取查询返回的第一行——如果没有结果我们将得到 None，然后我们可以将用户返回到登录页面并显示错误消息。假设我们请求的是一个有效用户——接下来我们将检查分配给该用户的密码是否与提交的密码相同。如果相同，我们将生成要发送给用户的验证代码，该代码将存储在数据库的 verification 表中，直到使用或过期。我们需要创建一个新的游标将验证代码插入到我们的表中。执行语句后，我们需要提交对数据库的更改，我们使用 `db.commit()` 来实现——然后我们将查询结果添加到我们的 session 中，以便以后可以对照检查。(图 03)

## 07 发送验证代码

现在我们认为正在处理一个有效用户，是时候进行双步流程的第二步了。在我们将变量存储到 session 之后的那一行，我们调用 `sendVerificationCode(VERIFICATION CODE, USER PHONE NUMBER)` 并传递我们想要发送给用户的代码和用户的电话号码。那么这个函数到底是什么样子的？它必须又大又长又复杂，因为它处理电信网络，对吧？错了。使用 Twilio 发送短信实际上非常简单。事实上，Twilio 的固有美感之一就在于其简单性。要发送一条短信，我们只需要做：

```
def sendVerificationCode(code, number):
    text = client.messages.create(
        body="Your verification code is:" + code,
        to=number,
        from="+YOURTWILIONUMBER"
    )
    return text.sid
```

使用我们用来实例化 Twilio REST 模块的 `client` 变量，我们可以访问 `messages` 类并执行 `create` 方法。我们只需要传递将构成消息正文的文本、我们想要发送到的号码以及我们想要发送的号码。当输入我们想要发送到的号码时，最好使用 `+CountryCode` 类型的电话号码，以避免对预期接收者产生任何歧义。我们发送的号码是我们的 Twilio 号码；只要它有余额，你就可以使用分配给你的任何 Twilio 号码。一旦我们执行该代码，消息将被发送，你的短信将直接发送到电话。SID 是发送的消息/通话的唯一标识符；收到它意味着消息已成功执行。

## 08 检查验证代码

此时用户将收到一条类似“Your verification code is: 12cd56”的短信，并将被呈现验证页面。如果此时他们选择浏览我们的网站，他们将无法访问我们不希望他们访问的任何内容。尽管如此，我们会知道他们已登录，因此如果他们返回验证页面，我们只需让他们输入代码。一旦他们提交代码，它将被发送到 `/check-code` 端点。

就像之前检查用户有效性时一样，我们将尝试检索验证代码并进行检查。(图 04)

首先我们将简单地检索代码并检查它分配的用户。如果该代码分配的用户与我们 session 中的用户匹配，那么我们可以确定正确的人正在使用正确的代码登录——如果不匹配，我们可以相应地重定向他们。

假设代码正确，我们需要检查它是否仍然有效。在第 6 步中，我们创建了一个过期时间，该时间比代码生成时晚五分钟。如果已超过五分钟（或你设置的任何时间），我们将认为它无效，删除表中的代码，然后注销用户以便他们重新开始，如下所示。

```
elif time.time() > expirationTime:
    expirySQL = db.cursor()
    expirySQL.execute("DELETE FROM verification WHERE code=%s", (codeToCheck,))
```

