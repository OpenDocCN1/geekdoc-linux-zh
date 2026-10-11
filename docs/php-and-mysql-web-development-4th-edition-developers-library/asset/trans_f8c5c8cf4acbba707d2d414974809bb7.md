

## 第9章 使用 PHP 编写 MySQL 程序

### 9.2.1.2 显示和输入成绩

现在，我们已经有了便捷提取 Web 输入参数的支持，可以利用该支持来编写 *score\_entry.php*。该脚本需要能够从自身的一次调用中传递信息给下一次调用。我们将使用一个名为 *action* 的参数来实现这一点，当脚本执行时，可以按如下方式获取该参数：

```php
$action = script_param('action');
```

如果该参数未设置，这意味着脚本是首次被调用。否则，它可以测试 *$action* 的值以确定要执行的操作。*score\_entry.php* 的一般框架如下所示：

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

$action 变量可以取几个值，我们在 switch 语句中对其进行测试。在 PHP 中，switch 与其 C 语言对应物非常相似；此处用于确定采取哪个动作并调用实现该动作的函数。为了避免使用字面动作值，switch 语句引用了之前在脚本中使用 PHP 的 `define()` 结构设置的符号动作名称。

让我们逐一检查处理这些动作的函数。第一个函数 `display_events()` 通过从 MySQL 检索 `grade_event` 表的行并显示它们，呈现允许事件的列表。表的每一行列出事件 ID、日期和事件类别（测试或测验）。事件 ID 以超链接的形式出现在页面上，你可以选择它来编辑该事件的分数。在事件行之后，该函数添加另一行，包含一个允许创建新事件的链接：

```php
function display_events($dbh)
{
    print("Select an event by clicking on its number, or select\n");
    print("New Event to create a new grade event:<br /><br />\n\n");
    print("<table border=\"1\">\n");

    # 打印一行表格列标题
    print("<tr>\n");
    display_cell('th', 'Event ID');
    display_cell('th', 'Date');
    display_cell('th', 'Category');
    print("</tr>\n");

    # 呈现现有事件列表。将每个事件 ID 与一个显示该事件分数的链接关联。
    $stmt = "SELECT event_id, date, category
              FROM grade_event ORDER BY event_id";
    $sth = $dbh->query($stmt);

    while ($row = $sth->fetch())
    {
        print("<tr>\n");
        $uri = sprintf("%s?action=%d&event_id=%d",
                       script_name(),
                       DISPLAY_SCORES,
                       $row['event_id']);
        display_cell('td',
                     "<a href=\"$uri\">" . $row['event_id'] . "</a>",
                     FALSE);
        display_cell('td', $row['date']);
        display_cell('td', $row['category']);
        print("</tr>\n");
    }

    # 添加一个用于创建新事件的链接
    print("<tr align='center'>\n");
    $uri = sprintf("%s?action=%d",
                  script_name(),
                  SOLICIT_EVENT);
    display_cell('td colspan="3"',
                 "<a href=\"$uri\">Create New Event</a>",
                 FALSE);
    print("</tr>\n");

    print("</table>\n");
}
```

重新调用 `score_entry.php` 的超链接 URL 是使用 `script_name()` 构造的，该函数用于确定脚本自身的路径名。`script_name()` 非常有用，因为它使你可以避免将脚本名称硬编码到代码中。（如果你直接写明脚本名称，那么当你重命名该脚本时，代码就会失效。）可以在 `samp/db_pdo.php` 文件中找到 `script_name()`。

`script_name()` 与 `script_param()` 有些相似，因为它访问一个 PHP 超全局数组。然而，它使用不同的数组，因为脚本名称是 Web 服务器提供的信息的一部分，而不是输入参数的一部分。

```php
function script_name()
{
    return ($_SERVER["SCRIPT_NAME"]);
}
```

`display_events()` 使用的 `display_cell()` 函数生成事件表格中的单元格：

```php
# 显示 HTML 表格的一个单元格。$tag 是标签名称（'th' 或 'td'
# 分别代表标题或数据单元格），$value 是要显示的值，
# $encode 应为 true 或 false，指示是否在显示值之前对其进行 HTML 编码。
# $encode 是可选的，默认为 true。
function display_cell($tag, $value, $encode = TRUE) {
    if (strlen($value) == 0) { # 值是否为空/未设置？
        $value = '&nbsp;';
    } else if ($encode) { # 如果请求则执行 HTML 编码
        $value = htmlentities($value);
    }
    print "<$tag>$value</$tag>\n";
}
```

如果你在 `display_events()` 呈现的表格中选择“Create New Event”链接，`score_entry.php` 将以 `SOLICIT_EVENT` 动作再次被调用。这会触发对 `solicit_event_info()` 的调用，该函数显示一个表单，使你可以输入新事件的日期和类别：

```php
function solicit_event_info() {
    print ("<form method='post' action='".script_name()."'>\n"
           . "<input type='hidden' name='action' value='"
             . ADD_EVENT . "'>\n");
    print 'Enter information for new grade event:<br /><br />\n';
    print 'Date: \n';
    print "<input type='text' name='date' value='' size='10'> \n\n";
    print '<br />\n';
    print 'Category: \n';
    print "<input type='radio' name='category' value='T' checked='checked'>\n";
    print " Test \n";
    print "<input type='radio' name='category' value='Q'>\n";
    print " Quiz \n";
    print "<input type='submit' name='submit' value='Submit'> \n\n";
    print '</form>\n';
}
```

`Solicit_event_info()` 生成的表单包含一个用于输入日期的编辑字段、一对用于指定新事件是测试还是测验的单选按钮，以及一个 Submit 按钮。默认事件类别为 'T'（测试）。脚本在此处输出字面 HTML 来构建表单。对于本章后续的脚本，我们将开发一组生成表单元素的辅助函数。

当你填写此表单并提交时，`score_entry.php` 再次被调用，这次 `action` 值等于 `ADD_EVENT`。然后调用 `add_new_event()` 函数以向 `grade_event` 表中插入新行：

```php
function add_new_event($dbh)
{
    $date = script_param('date');       # 获取日期和事件类别
    $category = script_param('category'); # 由用户输入

    if (empty($date)) # 确保已输入日期，且为 ISO 8601 格式
        die("No date specified\n");
    if (!preg_match('/^\d{4}-\d{1,2}-\d{1,2}$/', $date))
        die("Please enter the date in ISO 8601 format (CCYY-MM-DD)\n");
    if ($category != 'T' && $category != 'Q')
        die("Bad event category\n");

    $stmt = "INSERT INTO grade_event (date, category) VALUES(?, ?)";
    $sth = $dbh->prepare($stmt);
    $sth->execute(array($date, $category));
}
```

`add_new_event()` 使用 `script_param()` 库例程来访问对应于新事件录入表单中日期和类别字段的参数值。然后执行一些最基本的安全检查：

- 日期不应为空，并且应以 ISO 8601 格式输入。`preg_match()` 函数执行 ISO 8601 格式的图案匹配：`preg_match('/^\d{4}-\d{1,2}-\d{1,2}$/', $date)`

  这里使用单引号，以防止美元符号和反斜杠被解释为特殊字符。如果日期由三组数字组成，且它们由非数字字符分隔，则测试结果为真。这虽然不能保证万无一失，但很容易添加到脚本中，并且可以捕捉到许多常见错误。

- 事件类别必须是 `grade_event` 表中 `category` 列允许的其中一个值（'T' 或 'Q'）。

为了增加安全性，你可能希望在插入数据之前通过设置 `SQL` 模式来启用输入数据限制。例如：

```php
$dbh->exec('SET sql_mode = "TRADITIONAL"');
```

如果参数值看起来正常，`add_new_event()` 将新行插入 `grade_event` 表。语句执行代码使用占位符，确保数据值在插入查询字符串时被正确引用。执行语句后，`add_new_event()` 返回脚本的主部分（`switch` 语句），该部分再次显示事件列表，以便你可以选择新事件并开始为其输入分数。

