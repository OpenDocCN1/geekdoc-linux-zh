
## 数据库抽象 209

此示例与 PHP 4.0 示例的唯一区别在于 PHPLib 使用了面向对象的方法。

与 PHP 4.0 会话库一样，PHPLib 使用存储模块（在 PHPLib 术语中称为容器，containers）来存储会话数据。容器类都以 `CT_prefix` 开头。SQL 数据库是存储会话数据最常见的方式，但 PHPLib 也支持其他类。

PHPLib 7.2 中可用容器类如下：

- `CT_Sql` 是默认容器，并将会话数据存储在数据库中。它包含以下类：

| 名字 | 描述 |
| --- | --- |
| `$database_class` | `DB_Sql` 类的名称，应用于连接到数据库。 |
| `$database_table` | 用于存储会话数据的表名。 |
| `$encoding_mode` | 此变量控制会话数据的存储方式。它可以接受两个值：base64 或 slashes（斜杠）。通常情况下，你不应该更改默认值（base64）；这样，会话数据在存储到数据库之前会用 Base64 进行编码。为了调试目的，你可能希望使用另一种方法 slashes，将会话数据以明文形式存储在表中。 |

- 在功能方面，`CT_Split_Sql` 与 `CT_Sql` 相同。如果底层数据库无法在一个字段中存储足够的会话数据，特别是当数据库处理二进制大对象（BLOBs）存在问题时，则必须使用 `CT_Split_Sql`。`CT_Split_Sql` 与 `CT_Sql` 的表不兼容。

要更改类拆分会话数据的长度，你可以使用变量 `$split_length`，其默认值为 4096 (KB)。

- `Shm` 将会话数据存储在共享内存中。为了使用此功能，你需要一个编译了支持共享内存的 PHP。该容器更快，因为它将数据存储在可以直接访问的内存中。缺点是，如果你由于任何原因必须重启服务器，所有会话数据都将丢失。此外，由于内存消耗，并发会话的数量受到限制。每个会话占用一定的内存（内存取决于会话变量的数量和大小），在所有可用内存被消耗后，将无法创建新的会话。

### 210 第 6 章 使用 PHP 访问数据库

这些类变量与 `CT_Sql` 的不同：

| 参数 | 描述 |
| --- | --- |
| `$max_sessions` | 最大同时活动会话数。当前默认值为 500。 |
| `$shm_key` | 应该使用的共享内存段的唯一键。确保每个应用程序的此键是唯一的至关重要。 |
| `$shm_size` | 共享内存段的大小（单位为字节）。此大小可以通过公式 `shm_size = max_sessions * session_size` 进行近似计算，其中会话大小平均约为 600 字节。默认值为 64000 (64KB)。 |

- `CT_Dbm` 使用 UNIX DBM 文件存储数据。这种类型的数据库以键/值对的形式将数据存储在系统上的普通文件中。你应该设置的唯一变量是 `$dbm_file`，即 DBM 文件的文件名。该文件必须存在且权限正确；服务器需要对其拥有写权限。
- `CT_ldap` 将数据存储在 LDAP（轻量级目录访问协议）服务器中。PHP 必须编译了 LDAP 支持才能使用此容器。`CT_ldap` 类具有以下属性：

| 项目 | 描述 |
| --- | --- |
| `$ldap_host`, `$ldap_port` | LDAP 服务器的主机名和端口号。 |
| `$rootdn`, `$rootpw` | LDAP 服务器的根区分名（DN）和密码，用于连接到服务器。 |
| `$basedn` | 会话数据应存储在此区分名之下。 |
| `$objclass` | 对象类的名称（可以与 SQL 表名比较）。 |

在查看 `local.inc` 时，你将看到一系列类定义；其中三个实际上与我们的示例有关：

```php
class DB_Example extends DB_Sql {
var $Host = 'localhost';
var $database = 'phplib';
var $User = 'tobias';
var $Password = 'justdoit';
}
```

```php
class Example_CT_Sql extends CT_Sql {
var $database_class = "DB_Example"; // 连接到哪个数据库...
var $database_table = "active_sessions"; // 并在其中查找我们的会话数据
}
```

```php
class Example_Session extends Session {
var $classname = "Example_Session";
var $cookename = ""; // 默认为 classname
var $magic = "ococulus"; // ID 种子
var $mode = "cookie"; // 我们通过 cookie 传播 session ID
var $fallback_mode = "get"; // 0 = 使用会话 cookie，否则为分钟
var $lifetime = 0; // 直到会话过期
var $that_class = "Example_CT_Sql"; // 数据存储容器的名称
var $gc_probability = 5;
}
```

如所示，这些类之间存在关系；在 `Example_Session` 类中，变量 `$that_class` 被设置为 `Example_CT_Sql` 类的名称，而在 `Example_CT_Sql` 中，`$database_class` 变量指向 `DB_Sql` 类。图 6.1 详细显示了这种关系。

![](img/eddeabf7128be657d5f725f)

### 214 第 6 章 使用 PHP 访问数据库

- 验证范围不仅限于目录，还可以针对应用程序的单个文件进行设置，甚至可以在脚本内部实现身份验证级别。你可以向无访问权限的用户隐藏脚本的部分内容。

- 系统未识别的用户可以在登录前注册。系统会提供注册表单，PHPLib 会自动在用户数据库中创建一个标准条目。

- 即使是 CGI 版本的 PHP，通过 PHPLib 进行验证同样有效。

- 你可以安全地退出。这意味着你可以给用户终止当前会话的机会（一个注销按钮）。

- 用户可以在特定的空闲时间后自动注销。这样做为你的应用程序提供了额外的安全性，可以防止长时间空闲后发生会话劫持。

### Auth 示例

让我们来看一个基础示例。列表 6.4 中的示例展示了当你第一次调用它时 PHPLib 的默认登录界面。使用 PHPLib 默认的用户名/密码对 `user/test` 进行登录。通过验证后，你将看到你的 ID、用户名和权限。

列表 6.4 如何使用 Auth 的基础示例

```php
page_open(array('sess' => "Example_Session", "auth" => "Example_Auth"));
printf("Your session: %s<br>\n", $sess->id);
printf("Your User ID: %s<br>\n", $auth['uid']);
printf("Your user name: %s<br>\n", $auth['uname']);
printf("Your permissions: %s<br>\n", $auth['perm']);
page_close();
```

所有使用 PHPLib 验证的页面都遵循这一通用结构。首先调用 `page_open()`；只有在用户登录并通过验证后，才会执行脚本的其余部分。你可以安全地确保任何用户在未登录的情况下都不会看到 `page_open()` 之后的任何内容。通过单行的 `page_open()` 调用，你就为脚本添加了完整的用户身份验证。在建立了你在应用程序中想要使用的类之后，PHPLib 确实是一个易于使用的库。到目前为止，我们的示例使用了 PHPLib 分发包提供的示例类。但在工作中，你可能需要创建自己的类（派自基类）以更好地适应你的需求。为此，有必要进一步了解 PHPLib 的内部工作原理。

### 验证 215

#### Auth 内部原理

假设你使用 MySQL 作为数据库引擎，以下架构将用于用户表：

```sql
CREATE TABLE auth_user (
  user_id varchar(32) NOT NULL,
  username varchar(32) NOT NULL,
  password varchar(32) NOT NULL,
  perms varchar(255),
  PRIMARY KEY (user_id),
  UNIQUE k_username (username)
);
```

主键是 `user_id`，因为 PHPLib 内部处理的是这个 ID，而不是用户的用户名/密码对。这个 ID（由 PHPLib 调用）是一个唯一字符串，类似于话 ID，通过 `uniqid()` 和 `md5()` 组合创建：
`id = md5(uniqid($hash_secret));`

为什么 PHPLib 不使用标识 `username` 和 `password` 字段的复合主键呢？这样就可以节省额外的 `user_id` 字段。原因为 PHPLib 的目标是支持任何身份验证过程并使接口尽可能简单。为每个用户提供一个独立的、固定长度的唯一标识符，方便在关系模型中创建与 `auth_user` 表关联的附加表。

我们上一个示例中的技巧是简单使用了 PHPLib 分发包中 `Example_Default_Auth` 提供的 Auth 类的默认实现。你总是需要编写自己扩展 `Auth` 基类的类。在它的核心形式上，Auth 是不可用的，因为它没有提供验证所需的两个函数。Auth 既不知道你希望登录界面看起来什么样，也不知道你希望如何处理验证。因此，它不会尝试为你完成，你必须在派生类中自己定义这些函数。列表 6.5 显示了此类派生类的示例，它与 `Local.inc` 中的示例实现类似。

### 列表 6.5 扩展 Auth 基类

```php
require("EasyTemplate.php3");
class My_Auth extends Auth
{
  $classname = "My_Auth";
  $database_class = "DB_Example";
  $database_table = "auth_user";
  function auth_loginform()
  {
    // 创建模板实例
    $tpl = new EasyTemplate("loginform.inc.html");
```

### 216 第 6 章 使用 PHP 访问数据库

### 列表 6.5 续

```php
// 用户名是否已设置？如果是，意味着
// 第一次验证尝试失败了。
if(isset($this->auth['uname']))
{
    $tpl->assign("USERNAME", $this->auth['uname']);
    $tpl->assign("MESSAGE", "您的用户名或密码无效\n无效。<Br> 请重试！");
} else {
    $tpl->assign("USERNAME", "");
    $tpl->assign("MESSAGE", "请使用用户名和\n密码识别您的身份：");
}
// ... (其余代码)
function auth_login()
{
    // 全局变量
    global $username, $password;
    // 如果用户名已设置
    if(isset($this->auth['uname']))
    {
        $this->auth['uname'] = $username;
    }
    // 将 uid 设置为 false
    $uid = false;
    // 查询数据库
    $query = "SELECT * FROM auth_user
              WHERE username = '$username'
              AND password = '$password'";
    // 执行查询
    $this->db->query($query);
    // 如果返回了一行
    if($this->db->num_rows() == 1)
    {
        // 获取记录
        $this->db->next();
        // 设置 uid
        $uid = $this->row['user_id'];
        // 填充 auth 数组
        $this->auth['uid'] = $uid;
        $this->auth['uname'] = $this->row['username'];
        $this->auth['perm'] = $this->row['perms'];
    }
    return $uid;
}
```
*(注：列表 6.5 续部分的 OCR 文本片段破碎且损坏；我已根据提供的片段和标准的 PHP/Auth 模式重建了逻辑流，以确保其功能性表示。)*

# 列表 6.6 使用 Perm 类。

```
page_open(array("sess" => "Example_Session", "auth" => "Example_Auth",
    "perm" => "Example_Perm"));
```

```php
if(isset($mode) && $mode == "reload") {
    $auth->unauth();
    print('You have been logged out.<br>');
    printf('If you want, you can <a href="%s"> login again.',
    $sess->url(basename(PHP_SELF)));
} else {
    if($perm->have_perm('admin')) {
        print('<cb-Welcome Admin.</<br><br>');
        print('You are logged in with "admin" permissions.<br>');
    } else {
        printf('You are logged with "%s" permissions.<br>',
        $auth->auth['perm']);
    }
    printf('Your name: %s<br>', $auth->auth['username']);
    printf('<a href="%s">Log out</a>',
    $sess->url(basename(PHP_SELF))."&mode=reload"));
}
```

```php
page_close();
```

### 位操作 (Bit Bashing)

位运算通常会让新手程序员感到非常困惑，即使是高级开发者偶尔也会在处理时遇到困难。将标志表示为位模式非常有用；尽管 PHPLib 将此用于权限级别。它也被用于在数据库的单个 INT 字段中存储标志值。考虑一个需要跟踪多个不同状态的应用，例如用户的爱好。与其在数据库中为每个爱好设置一个字段并将其设置为真或假，你只需要一个标志字段。根据用户是否拥有某个特定爱好，该爱好的位就会开启或关闭。简单来说，位操作是同时操纵一个或多个位的操作。你知道在二进制系统中，你拥有字节位（octets）——一系列的 0 和 1。二进制系统中的十数字 42 表示为 00101010：

```
Bit position: 7 6 5 4 3 2 1 0
Bit value: 0 0 1 0 1 0 1 0
```

最右侧的位 0 称为最低位（Least Significant Bit）。位 7 称为最高位（Most Significant Bit）。要从二进制系统转换为十进制系统以及反之，你可以使用 PHP 中的 `bin()` 和 `decBin()`。二进制运算符可以在这些位之间切换开启或关闭。

#### 设置位 (Setting a Bit)

要设置值中的某位，你可以使用包含或运算（value | value）。例如，如果标志的值为 3（意味着第一位和第二位已设置），而你想设置第二位（记住，位计数从 0 开始），你将当前值与 4（2 的二次方）进行或 运算。

```php
$value = 3;
$value |= 4;
```

结果为 7。在二进制系统中，该操作如下：

```
0 0 0 0 1 1
| 0 0 0 0 1 0
= 0 0 0 0 1 1
```

#### 翻转位 (Toggling a Bit)

翻转位——如果是 0 则变为 1，反之亦然——是使用异或（XOR）运算符（value ^ value）。如果你的值为 3，我们想翻转第一位（当前为 1：0000010），将使用以下行：

```php
$value = 3;
$value ^= 2;
```

结果将是 1。在二进制中：

```
0 0 0 0 1 0
^ 0 0 0 0 1 0
= 0 0 0 0 0 0
```

#### 清除位 (Clearing a Bit)

清除位简单的方法是确保该位是开启状态，然后对其进行取反。这需要两个位运算符：取反（INVERSE）和与（value & -value）。要清除值 3 中的第一位，可以使用此行：

```php
$value = 3;
$value &= -2;
```

#### 测试位 (Testing for a Bit)

要测试值中的某位是否已设置，你使用逻辑与运算符。它比较两个值；如果两个位都是 1，它返回 1。例如，要测试值 3 中的第一位是否已设置，你可以使用以下代码：

```php
if(2 & 3)
```
