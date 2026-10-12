
## Site Security

注意，你并不是简单地创建一个字段来存储用户的明文密码，而是创建字段来存储用户密码的单向哈希值。这样做确保了密码仍可以与在密码提示处输入的值进行比较，但使得试图在数据库泄露时破解密码的人变得极其困难。如果你熟悉 MD5 或 SHA1，你知道它们都是单向哈希算法。在通过其中任何一种算法进行哈希处理后，几乎不可能确定原始密码。

> MD5 获取输入字符串并创建原始输入的 128 位“唯一”指纹，即哈希值。SHA1 的行为类似，但稍具安全性，生成 160 位“唯一”指纹。

你可能注意到，之前的讨论在关于这两种解决方案提供的唯一性或防破解哈希的绝对性方面并没有说得绝对。直到最近，MD5 一直被认为是对除最安全数据外所有数据进行哈希处理的合理解决方案，SHA1 也是如此。当使用暴力破解时，没有哪种加密方案是 100% 无法被破解的。一个密码生成程序可以遍历每个字符和每个密码长度的所有组合，直到最终找到一个与这两种算法之一产生的哈希值匹配的输入字符串。

然而，密码分析的最新进展证明，MD5 可以被更快击败，方法是找到一个产生相同输出哈希值的输入，即使输入字符串不匹配——这是 MD5 的固有弱点。最近，SHA1 也受到了攻击，而且随着处理能力的提高，暴力破解哈希所需的时间迅速减少。

为了对抗 MD5 中看到的任何类型的碰撞攻击，你创建了 Users 表来保存密码的 MD5 和 SHA1 哈希值。这样做有效地使任何碰撞攻击尝试变得徒劳——即使入侵者设法找到一个与 MD5 哈希值匹配的输入字符串，除非它是真实密码，否则它将不会与 SHA1 哈希值匹配。

为了使数据库对认证脚本有用，你需要至少添加一个用户：

```sql
INSERT INTO Users VALUES ('testuser', MD5('testpass'), SHA1('testpass'));
```

注意，在添加密码时使用了内置的 MySQL 函数 MD5() 和 SHA1()。

### A PHP Basic Authentication Script

一旦你的数据库设置好，创建以下脚本，并将其保存为 `phpauthbasic.php`：

```php
<?php
  // Define database constants
  define('AUTH_HOST', 'localhost');
  define('AUTH_USER', 'WebAuth');
  define('AUTH_PASS', 'AuthPass');
  define('AUTH_DB', 'WebAuth');
  
  function attempt_auth() {
    // Send authentication headers
    header('WWW-Authenticate: Basic realm="Protected by PHP"');
    header('HTTP/1.0 401 Unauthorized');
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

          return $ret;
      }
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
      exit;
  }
?>
```

168

## Site Security

这一切意味着什么？看看是什么让这段脚本运行起来的。

你要做的第一件事是为数据库连接定义一些常量：

```php
<?php
// Define database constants
define('AUTH_HOST', 'localhost');
define('AUTH_USER', 'WebAuth');
define('AUTH_PASS', 'AuthPass');
define('AUTH_DB', 'WebAuth');
```

接下来是 `attempt_auth()` 的函数定义。这个函数只是发送响应头给浏览器，告诉它尝试进行基本身份验证登录，并将给定的 realm 显示为登录提示中的安全区域：

```php
function attempt_auth()
{
    // Send authentication headers
    header('WWW-Authenticate: Basic realm="Protected by PHP"');
    header('HTTP/1.0 401 Unauthorized');
}
```

在 `attempt_auth()` 之后是 `check_login()` 的函数定义。这是将传入的用户名和密码实际与之前创建的 WebAuth 数据库中存储的值进行检查的地方。首先要确保传入了用户名和密码，并连接到数据库并设置 WebAuth 为活动状态：

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

在建立数据库连接后，你执行一个查询来检查用户名/密码是否匹配：

```php
// Search for matches
$result =
    mysql_query("SELECT COUNT(username) AS ucount
                FROM Users
                WHERE username='" . addslashes($username) . "'
                    AND passwd_md5='" . md5($password) . "'
                    AND passwd_sha1='" . sha1($password) . "'",
                $conn);
```

为了构建这个查询，首先必须使用 `addslashes()` 转义用户名，以帮助避免任何 SQL 注入攻击（稍后讨论）。这里使用了 PHP 函数 `md5()` 和 `sha1()`，但如果你愿意，可以很容易地使用 MySQL 的等价物——它们应该产生完全相同的结果：

```php
// Search for matches
$result =
    mysql_query("SELECT COUNT(username) AS count
                FROM Users
                WHERE username='" . addslashes($username) . "'
                    AND passwd_md5=MD5('" . addslashes($password) . "')
                    AND passwd_sha1=SHA1('" . addslashes($password) . "')",
                $conn);
```

你可能注意到，`addslashes()` 函数被添加为密码的包装器，而在之前 PHP 执行密码哈希的情况下并不存在。这也是为了防止任何 SQL 注入攻击，甚至是用户密码中包含撇号的简单错误。当首先使用 PHP 对密码进行哈希处理时，没有必要使用 `addslashes()` 转义结果，因为 `md5()` 和 `sha1()` 函数产生的输出仅由十六进制值组成——不可能有撇号或其他危险字符漏网。

为了完成 `check_login()` 函数，将返回占位符设置为 `true`，并创建一个会话变量，你将在脚本后面使用它以避免不必要的重复查询：

```php
// Check if a match was found
if (($row = mysql_fetch_array($result)) && $row['count'])
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

接下来是脚本中实际首次被解释的代码，你通过初始化会话数据开始：

```php
session_start();
```

然后首先检查 `check_login()` 中的会话变量是否已设置。如果尚未设置——意味着此人尚未通过身份验证——检查 `PHP_AUTH_USER` 服务器变量并调用 `check_login()` 函数。当 PHP 尝试使用基本身份验证获取登录信息时，服务器变量 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 都存在。如果它们未设置，用户尚未被提示提供登录信息。在这种情况下，如果没有传递登录信息且之前传递的身份验证无效，则希望提示用户输入登录信息。如果找不到有效的用户信息，将调用 `attempt_auth()`，用户将有机会再次登录。只有当用户在登录提示上点击取消时，才会显示“需要授权”的消息：
