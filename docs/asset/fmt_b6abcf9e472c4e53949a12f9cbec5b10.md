
```php
<?php
require_once('date.php');

$currweek = new Date();

$weeksleft = 52 - ($currweek->getWeekOfYear());
echo "There are " . $weeksleft . " weeks left in the year.";
?>
```

如您所见，当您试图完成更复杂的日期计算或处理时区时，如此简单的东西确实可以让您的生活更容易。

## DB

这是允许您轻松连接和查询数据库的 PEAR 包。还有许多其他与数据库相关的包可供您参考。例如，`MDB` 与 `DB` 类似，但提供了更多可移植性。`DB` 应能在您的标准配置上运行，但如果您遇到兼容性问题，还可以尝试其他方案。实际上，PEAR 专门设立了一个用于处理数据库的包类别，可以通过 `http://pear.php.net/packages.php?catpid=7&catname=Database` 找到。

在接下来几个示例中，您需要以下信息：

- `MySQL`：您的数据库类型
- `testdatabase`：数据库名称
- `testtable`：数据库表
- `username`：访问数据库的用户名
- `password`：用户的密码
- `localhost`：服务器名称
- `field1, field2`：您将要查询的字段

这将有助于在自定义安装包时“填空”。

### 连接数据库

为了连接到数据库，您需要向新的数据库对象传递正确的数据源名称 `DSN`。语法如下：

```php
<?php
require_once("db.php");
$dsn = "mysql://username:password@localhost/testdatabase";
$db = DB::connect($dsn);
if (PEAR::isError($db)) {
    die($db->getMessage());
}
echo "Connected successfully. Now what?";
?>
```

如您所见，这就是连接所需的全部，更重要的是，它报告了过程中可能发生的任何错误。再次说明，请随意访问官方 PEAR 文档以获取关于连接数据库时可设置的各种选项（如端口号或协议）的详细说明。此文档可在 `http://pear.php.net/manual/en/package.database.db.intro-connect.php` 找到。现在，试着查询想象中的表中想象中的字段。

### 查询数据库

要查询数据库，您需要传递表名和所需的过滤器，因此输入以下内容：

```php
<?php
require_once("db.php");
$dsn = "mysql://username:password@localhost/testdatabase";

$db = DB::connect($dsn);
if (PEAR::isError($db)) {
    die($db->getMessage());
}

//query
$res =& $db->query('SELECT * FROM testtable');

//display number of rows
echo "There were " . $res->numRows() . " rows found.";

//display one column of results, or by row number
while ($row =& $res->fetchRow()) {
    echo $row[0] . "\n";
}

//display more than one field of results
//also switching Associative mode
while ($res->fetchInto($row, DB_FETCHMODE_ASSOC)) {
    echo $row['field1'] . "," . $row['field2'] . "\n";
}
?>
```

这只是该包的一个示例。您还能用它做很多其他事情，例如获取多个查询的结果集，以及自动准备和执行常用的 SQL 语句。

## HTML_CSS 和 HTML_Page

这些包允许您动态创建 CSS 样式表，并轻松地将它们集成到新的 HTML 页面中。`HTML_Page` 还可以为您执行其他功能，但本示例专注于创建新的 CSS 样式表：

```php
<?php
require_once('HTML/CSS.php');
require_once('HTML/Page.php');

$css = new HTML_CSS();

//set the styles
$css->setStyle('body', 'background-color', '#FF00CC');
$css->setStyle('body', 'color', '#ffffff');
$css->setStyle('h1', 'text-align', 'center');
$css->setStyle('h1', 'font', '16pt erdama');
$css->setStyle('p', 'font', '12pt verdana');

//create a new page
$p = new HTML_Page();

$p->setTitle("Testing the CSS");

$p->addStyleDeclaration($css, 'text/css');
$p->addBodyContent('<h1>Wow, this background is really bright!</h1>');
$p->addBodyContent('<p>This should wake you up.</p>');

$p->display();
?>
```

使用简单的 `if` 或 `switch` 语句，您可以使用类似上述内容来动态创建样式表，依据可以是个人的授权级别、使用的浏览器或操作系统类型、时间或日期，或者您能想到的任何其他因素。

## HTML_QuickForm

该包的目的是快速轻松地创建 HTML 表单。它易于使用，但相对功能强大，并允许您进行相当多的自定义。请看看一个快速示例：

```php
<?php
    require_once ("HTML/QuickForm.php");
    
    //create a new form object
    $form = new HTML_QuickForm('firstForm');
    
    //add two input fields; this is completely customizable
    $form->addElement('text', 'name', 'Your full name:', array('size' => 50,
        'maxlength' => 255));
    $form->addElement('text', 'email', 'Your email address:', array('size' => 50,
        'maxlength' => 255));
    
    //add a submit button
    $form->addElement('submit', null, 'Send');
    
    //add validation rules of our choosing
    //using addRule('field_to_be_validated', 'error_message to be displayed',
    // 'validation_type',
    $form->addRule('name', 'Empty Name Field', 'required', null, 'client');
    $form->addRule('email', 'Empty Email Address', 'required', null, 'client');
    $form->addRule('email', 'Incorrect Format for Email Address', 'email', null,
        'client');
    
    //check to make sure input followed all our rules
    //if so, put all form elements into an array for us
    //for sake of example, let's print the values
    if ($form->validate()) {
        $elements=$form->exportValues();
        print_r ($elements);
        exit;
    }
    
    //show the form
    $form->display();
?>
```
