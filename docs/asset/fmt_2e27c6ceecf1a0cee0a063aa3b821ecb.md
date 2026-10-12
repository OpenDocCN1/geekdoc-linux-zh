
```php
}

function check_login($username, $password)
{
    $ret = false;

    if ($username && $password)
    {
        // Check if login matches database values
        $conn = mysql_connect(AUTH_HOST, AUTH_USER, AUTH_PASS);

        if (mysql_select_db(AUTH_DB, $conn))
        {
            // Search for matches
            $result =
                mysql_query("SELECT COUNT(username) AS ucount
                             FROM Users
                             WHERE username='" . addslashes($username) . "'
                             AND passwd_md5='" . md5($password) . "'
                             AND passwd_sha1='" . sha1($password) . "'",
                             $conn);

            // Check if a match was found
            if (($row = mysql_fetch_array($result)) && $row['ucount'])
            {
                $ret = true;
                $_SESSION['username'] = $username;
            }

            // Close connection
            mysql_close($conn);
        }
    }

    return $ret;
}

session_start();

// Check if using valid credentials
if (!(isset($_SESSION['username']) ||
      (isset($_SERVER['PHP_AUTH_USER']) &&
       check_login($_SERVER['PHP_AUTH_USER'],
                   $_SERVER['PHP_AUTH_PW']))))
{
    // Show login prompt
    attempt_auth();
    echo 'Authorization Required';
    exit();
}
?>
```

这一切意味着什么？来看看是什么让这段脚本运转起来的。

## 配置数据库常量

你要做的第一件事是为数据库连接定义一些常量：

```php
<?php

// Define database constants

define('AUTH_HOST', 'localhost');

define('AUTH_USER', 'WebAuth');

define('AUTH_PASS', 'AuthPass');

define('AUTH_DB', 'WebAuth');
```

## `attempt_auth()` 函数

接下来是 `attempt_auth()` 的函数定义。该函数只需向浏览器发送响应头，告知其尝试进行 Basic 认证登录，并将给定的 realm（域）作为登录提示中的安全区域显示：

```php
function attempt_auth()
{
  // Send authentication headers
  header('WWW-Authenticate: Basic realm="Protected by PHP"');
  header('HTTP/1.0 401 Unauthorized');
}
```

## `check_login()` 函数定义

在 `attempt_auth()` 之后是 `check_login()` 的函数定义。这里将实际检查传入的用户名和密码，并与之前创建的 `WebAuth` 数据库中存储的值进行比对。首要任务是确保传入了用户名和密码，并连接到数据库，将 `WebAuth` 设为活动数据库：

```php
function check_login($username, $password)
{
	$ret = false;
	if ($username && $password)
	{
	  // Check if login matches database values
	  $conn = mysql_connect(AUTH_HOST, AUTH_USER, AUTH_PASS);
	  if (mysql_select_db(AUTH_DB, $conn))
	{
```

### 执行匹配查询

建立数据库连接后，执行查询以检查用户名/密码是否匹配：

```php
// Search for matches
$result =
mysql_query("SELECT COUNT(username) AS account
FROM users
WHERE username='$username'
AND password=md5('$password')
AND passwd_sha1='$sha1'", $conn);
```

要构建此查询，必须首先使用 `addslashes()` 转义用户名，以帮助避免任何 SQL 注入攻击（后文将讨论）。这里使用了 PHP 函数 `md5()` 和 `sha1()`，但如果你愿意，也可以轻松地使用 MySQL 的等效函数——它们应该会产生完全相同的结果：

```php
// Search for matches
$result =
mysql_query("SELECT COUNT(username) AS count
FROM users
WHERE username='" . addslashes($username) . "'
AND passwd_md5=MD5('" . addslashes($password) . "')
AND passwd_sha1=SHA1('" . addslashes($password) . "')",
$conn);
```

你可能已经注意到，`addslashes()` 函数被添加为密码的包装器，而在之前 PHP 进行密码哈希的情况下并没有这样做。这再次是为了防止 SQL 注入攻击，甚至防止用户在密码中包含单引号等简单错误导致的错误。当首先使用 PHP 对密码进行哈希处理时，无需使用 `addslashes()` 转义结果，因为 `md5()` 和 `sha1()` 函数产生的输出仅由十六进制值组成——不可能有单引号或其他危险字符混入。

### 完成 `check_login()`

为了完成 `check_login()` 函数，将返回占位符设置为 `true`，并创建一个稍后在脚本中使用的会话变量，以避免不必要的重复查询：

```php
// Check if a match was found
if (($row = mysql_fetch_array($result)) && $row['account'])
{
$ret = true;
$_SESSION['username'] = $username;
}

// Close connection
mysql_close($conn);
}

return $ret;
}
```

## 脚本主流程

进入脚本中实际首先被解释的代码，你首先初始化会话数据：

```php
session_start();
```

然后，你首先检查来自 `check_login()` 的会话变量是否已设置。如果尚未设置——意味着用户尚未通过身份验证——检查 PHP `USER` 和 `PHP_AUTH_PW` 服务器变量，并调用 `check_login()` 函数。当 PHP 尝试使用 Basic 认证获取登录信息时，服务器变量 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 都存在。如果未设置，说明用户尚未被提示输入登录信息。在这种情况下，如果没有传入信息且之前传入的凭据无效，你希望提示用户输入登录信息。如果未找到有效的用户信息，则调用 `attempt_auth()`，用户将获得再次登录的机会。只有当用户在登录提示上点击“取消”时，才会显示“Authorization Required”消息：
