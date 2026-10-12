
```php
function dvd_reserve_title($date, $title_id, $disk_id, $member_id) {

    global $db_conn, $err_msg;

    if (!$db_conn) {

        if (!($db_conn = dvd_open_db())) {

            return null;

        }

    }

    if ($result_id = pg_exec($db_conn, "insert into member_booking(member_id, title_id, date) values ($member_id, $title_id, '$date')") == false) {

        $err_msg = pg_errormessage($db_conn);

        return false;

    } else if ($result_id = pg_exec($db_conn, "update disk set member_id=$member_id where disk_id=$disk_id") == false) {

        $err_msg = pg_errormessage($db_conn);

        return false;

    } else {

        return true;

    }

}
```

572

# `dvd_reserve_title_cancel()`

此函数取消已预留的标题：

```php
function dvd_reserve_title_cancel($member_id) {
    global $db_conn, $err_msg;
    if (!$db_conn) {
        if (!$db_conn = dvd_open_db()) {
            return null;
        }
    }
    // 此函数假设 member_booking 表中成员只有一个预留
    if ($result_id = pg_exec($db_conn, "delete from member_booking where member_id=$member_id") == false) {
        $err_msg = pg_errormessage($db_conn);
        return false;
    } else if ($result_id = pg_exec($db_conn, "update disk set member_id=0 where member_id=$member_id") == false) {
        $err_msg = pg_errormessage($db_conn);
        return false;
    } else {
        return true;
    }
}
```

# `dvd_reserve_title_query_by_member()`

此函数查询特定成员预留的标题：

```php
function dvd_reserve_title_query_by_member($member_id, &$tmpTitle) {
    global $db_conn, $err_msg;
    // 获取数据库连接
    if (!$db_conn) {
        if (!$db_conn = dvd_open_db()) {
            return null;
        }
    }
    // 此函数假设 member_booking 表中成员只有一个预留
    if ($result_id = pg_exec($db_conn, "select * from member_booking where member_id=$member_id") == false) {
        $err_msg = pg_errormessage($db_conn);
        return false;
    } else if (pg_numRows($result_id) > 0) {
        $Member_booking_object = pg_Fetch_Object($result_id, 0);
        $tmpTitle = $Member_booking_object->title_id;
    } else {
        $tmpTitle = 0;
        return true;
    }
}
```

# 第 16 章

# `dvd_begin_transaction()`

此函数启动数据库事务：

```php
function dvd_begin_transaction() {
  global $db_conn;
  // 获取数据库连接
  if (!$db_conn) {
    if (!($db_conn = dvd_open_db())) {
      return null;
    }
  }
  return pg_exec($db_conn, "begin");
}
```

# `dvd_commit_transaction()`

此函数将数据库事务提交到数据库：

```php
function dvd_commit_transaction() {
  global $db_conn;
  // 获取数据库连接
  if (!$db_conn) {
    if (!($db_conn = dvd_open_db())) {
      return null;
    }
  }
  return pg_exec($db_conn, "commit");
}
```

下面的脚本包含了一些被其他脚本使用的通用定义和函数。下的大多数函数实现实现了将 HTML 渲染与应用程序业务逻辑分离的目标。

# `dvdstorecommon.php`

```php
// dvdstorecommon.php
// 其他脚本使用的函数和其他定义
require('dvdstoredbbffunctions.php');
```

574

这些常量用于区分来自“状态检查”例程或“搜索例程”的渲染函数调用：

```
define("FROM_STATUS", 0);
define("FROM_SEARCH", 1);
```

## `GenerateLoginForm()`

此函数使用 HTML 表单生成登录页面，其 action 脚本将对登录进行验证。请注意，当表单提交时，`$memberId` 和 `$lastName` 变量将供该 action 脚本使用：

```php
function GenerateLoginForm() {
    printf("<FORM METHOD=POST ACTION=dvdstorelogin.php\n");
    printf("<TABLE>
```

## `GenerateHTMLHeader()`

此函数仅用于显示一个头部消息。读者可以使用想象力，通过添加 HTML（包含图像、横幅等）来使其变得更加华丽：

```php
function GenerateHTMLHeader($message) {
    printf("<h1>%s</h1>\n", $message);
}
```

## `DisplayErrorMessage()`

此函数在 HTML 中显示错误消息。下方的 HTML 代码更多是为了适应页面格式设计，而不是为了可读性。基本上，它非常显眼地显示错误消息。它由需要向用户报告错误的其他函数调用：

```php
function DisplayErrorMessage($message) {
    printf("<BLOCKQUOTE><BLOCKQUOTE><H3>FONT COLOR=#cc0000%s</H3></BLOCKQUOTE></BLOCKQUOTE>\n", $message);
}
```

# 第 16 章

## `DisplaySearchMenu()`

此函数显示搜索菜单，以便商店用户可以搜索 DVD 数据库：

```php
function DisplaySearchMenu($MemberID) {
    $method = $_SERVER['REQUEST_METHOD'];
    printf("ACTION=dvdstoresearch.php?memberID=%s\n", $MemberID);
    printf("<TABLE\n");
```
