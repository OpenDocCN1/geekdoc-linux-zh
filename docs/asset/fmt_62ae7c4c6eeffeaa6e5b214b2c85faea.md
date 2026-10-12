
```php
<?php

session_start();

require("config.php");
require("functions.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($database, $db);

if($_POST['submit']) {
    $sql = "SELECT * FROM users WHERE username = '" .
    $_POST['username'] . "' AND password = '" .
    $_POST['password'] . "';";
    $result = mysql_query($sql);
    $numrows = mysql_num_rows($result);

    if($numrows == 1) {
        $row = mysql_fetch_assoc($result);
        if($row['active'] == 1) {
            session_register("USERNAME");
            session_register("USERID");
            $_SESSION['USERNAME'] = $row['username'];
            $_SESSION['USERID'] = $row['id'];

            switch($_GET['ref']) {
                case "newpost":
                    if(isset($_GET['id']) == FALSE) {
                        header("Location: " . $config_basedir .
                        "/newtopic.php");
                    }
                    else {
                        header("Location: " . $config_basedir .
                        "/newtopic.php?id=" . $_GET['id']);
                    }
                    break;

                case "reply":
                    if(isset($_GET['id']) == FALSE) {
                        header("Location: " . $config_basedir .
                        "/newtopic.php");
                    }
                    else {
                        header("Location: " . $config_basedir .
                        "/newtopic.php?id=" . $_GET['id']);
                    }
                    break;

                default:
                    header("Location: " . $config_basedir);
                    break;
            }
        }
        else {
            require("header.php");
            echo "This account is not verified yet. You were emailed a link to verify the account. Please click on the link in the email to continue.";
        }
    }
    else {
        header("Location: " . $config_basedir . "/login.php?error=1");
    }
} else {
    require("header.php");

    if($_GET['error']) {
        echo "Incorrect login, please try again!";
    }
?>
<form action="<?php echo pf_script_with_get($SCRIPT_NAME); ?>" method="post">

Don't have an account? Go and <a href="register.php">Register</a>!

<?php
}
require("footer.php");
?>
```

现在该执行必要的重定向了。请记住，需要用户登录的页面会重定向到登录页面，然后应重定向回原始页面。为了处理这种重定向，重定向到 `login.php` 的页面也会传递 `ref` GET 变量。该变量可能有两个取值：

- `newpost`。用户尝试创建新帖子。这应重定向到 `newtopic.php`。
- `reply`。用户尝试回复帖子。这应重定向到 `reply.php`。

如果发生登录错误，页面将被重定向，并添加 `error=1` 作为 GET 变量。这可以用来显示错误消息。

## 管理员登录

管理员登录页面在根本上与此前的页面相同。创建一个名为 `admin.php` 的新文件，并添加 `示例 5-3` 中所示的代码。

> **示例 5-3** 管理员登录页面与用户登录页面几乎相同。
