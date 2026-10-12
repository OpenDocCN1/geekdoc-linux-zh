
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

重新调用 `score_entry.php` 的超链接 URL 是使用 `script_name()` 构造的，该函数用于确定脚本自身的路径名。`script_name()` 非常有用，因为它使你可以避免将脚本名称硬编码到代码中。`如果你直接写明脚本名称，那么当你重命名该脚本时，代码就会失效。`可以在 `samp/db_pdo.php` 文件中找到 `script_name()`。

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
