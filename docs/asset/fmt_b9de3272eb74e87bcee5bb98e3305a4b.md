
`$_GET` 和 `$_POST` 是关联数组，元素以参数名称为键。例如，在 URL 中发送的 `action` 参数将作为 `$_GET['action']` 的值对 PHP 脚本可用。假设表单包含名为 `name` 和 `address` 的字段。当用户提交表单时，Web 服务器调用一个脚本处理表单内容。如果表单作为 `get` 请求提交，脚本可以通过检查 `$_GET['name']` 和 `$_GET['address']` 变量的值来找出表单中输入了哪些值。如果表单作为 `post` 请求提交，这些变量将位于 `$_POST['name']` 和 `$_POST['address']` 中。

对于包含大量字段的表单，给它们都赋予唯一的名称可能不太方便。PHP 使在表单中传入和传出数组变得容易。如果你使用诸如 `x[0]`、`x[1]` 等字段名称，PHP 会将它们存储在 `$_GET['x']` 或 `$_POST['x']` 中，其值本身将是一个数组。如果你将数组值赋给变量 `$x`，则数组元素可以用作 `$x[0]`、`$x[1]` 等。

在大多数情况下，我们不会关心参数是通过 `get` 还是 `post` 提交的，因此我们可以编写一个实用例程 `script_param()`，它接受一个参数名称，并检查这两个数组以找到参数值。如果参数不存在，该例程返回 `NULL`：

```php
function script_param($name)
{
    $val = NULL;
    if (isset ($_GET[$name]))
        $val = $_GET[$name];
    else if (isset ($_POST[$name]))
        $val = $_POST[$name];
    if (get_magic_quotes_gpc ())
        $val = remove_backslashes ($val);
    return ($val);
}
```

`script_param()` 使脚本能够通过名称轻松访问输入参数的值，而无需关心它们可能存储在哪个数组中。它还在提取参数值后对其进行处理，通过将该值传递给 `remove_backslashes()`。这样做的目的是适应启用了 `magic_quotes_gpc` 设置的配置，PHP 初始化文件中有一行如：

```ini
magic_quotes_gpc = On;
```

如果启用了该设置，PHP 会在参数值中添加反斜杠，以引用引号或反斜杠等特殊字符。额外的反斜杠使得检查参数值是否有效变得更加困难，因此 `remove_backslashes()` 将其去除。它使用递归算法实现，因为在 PHP 中有可能创建呈嵌套数组形式的参数：

```php
function remove_backslashes ($val)
{
  if (is_array ($val))
    {
      foreach ($val as $k => $v)
        $val[$k] = remove_backslashes ($v);
    }
  else if (!is_null ($val))
    $val = stripslashes ($val);
  return ($val);
}
```

### Web 输入参数与 register_globals

你可能熟悉 PHP 的 `register_globals` 配置设置，它使 Web 输入参数直接注册到脚本变量中。例如，名为 `x` 的表单字段或 URL 参数将直接存储到你脚本中名为 `$x` 的变量中。不幸的是，启用此功能意味着客户端可以以你未打算的方式设置你脚本中的变量。这是一个安全风险，因此 PHP 开发团队建议禁用 `register_globals`。`script_param()` 例程有意仅使用专门为输入参数提供的数组，这更安全，并且无论 `register_globals` 设置如何都能正常工作。

## 第9章 使用 PHP 编写 MySQL 程序

### 9.2.1.2 显示和输入成绩

现在，我们已经有了便捷提取 Web 输入参数的支持，可以利用该支持来编写 *score_entry.php*。该脚本需要能够从自身的一次调用中传递信息给下一次调用。我们将使用一个名为 *action* 的参数来实现这一点，当脚本执行时，可以按如下方式获取该参数：

```php
$action = script_param('action');
```

如果该参数未设置，这意味着脚本是首次被调用。否则，它可以测试 `$action` 的值以确定要执行的操作。*score_entry.php* 的一般框架如下所示：

```php
#!/usr/bin/php

# score_entry.php - 成绩管理项目的成绩录入脚本

require_once 'sampdb_pdo.php';

# 定义动作常量
define('SHOW_INITIAL_PAGE', 0);
define('SOLICIT_EVENT', 1);
define('ADD_EVENT', 2);
define('DISPLAY_SCORES', 3);
define('ENTER_SCORES', 4);

# ... 在此处放置输入处理函数 ...

$title = '成绩管理项目 -- 成绩录入';
html_begin($title, $title);

$dbh = sampdb_connect();

# 确定要执行的动作（如果未指定动作，默认显示初始页面）
$action = script_param('action');
if (is_null($action))
    $action = SHOW_INITIAL_PAGE;

switch ($action)
{
case SHOW_INITIAL_PAGE:     # 显示初始页面
    display_events($dbh);
    break;
case SOLICIT_EVENT:         # 请求新的事件信息
    solicit_event_info();
    break;
case ADD_EVENT:             # 向数据库添加新事件
    add_new_event($dbh);
    display_events($dbh);
    break;
case DISPLAY_SCORES:        # 显示所选事件的分数
    display_scores($dbh);
    break;
case ENTER_SCORES:          # 输入新分数或编辑后的分数
    enter_scores($dbh);
    display_events($dbh);
    break;
default:
    die("Unknown action code ($action)\n");
}

$dbh = NULL; # 关闭连接

html_end();
?>
```

`$action` 变量可以取几个值，我们在 `switch` 语句中对其进行测试。在 PHP 中，`switch` 与其 C 语言对应物非常相似；此处用于确定采取哪个动作并调用实现该动作的函数。为了避免使用字面动作值，`switch` 语句引用了之前在脚本中使用 PHP 的 `define()` 结构设置的符号动作名称。

让我们逐一检查处理这些动作的函数。第一个函数 `display_events()` 通过从 MySQL 检索 `grade_event` 表的行并显示它们，呈现允许事件的列表。表的每一行列出事件 ID、日期和事件类别（测试或测验）。事件 ID 以超链接的形式出现在页面上，你可以选择它来编辑该事件的分数。在事件行之后，该函数添加另一行，包含一个允许创建新事件的链接：
