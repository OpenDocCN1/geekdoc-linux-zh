
`nextFrame();`), `SWFBUTTON_MOUSEDOWN`);

然后将按钮添加到电影中并返回句柄。将按钮移动到图像正下方，并向电影添加一个新帧。然后生成必要的浏览器头信息，并输出电影：

### 将按钮添加到电影

```php
//将按钮添加到电影并保存返回的句柄

$handler = $aMovie->add($button);

//使用句柄将按钮移动到图像下方

$handler->moveTo(0,$h+3);

$aMovie->nextFrame();

//向浏览器发送适当的头信息

header("Content-Type:application/x-shockwave-flash");

//将电影输出到浏览器

$aMovie->output();
```

在使用 Ming 时，有几件事需要记住。首先，当你直接输出到浏览器时，必须在调用 `SWFMovie` 对象的 `output()` 方法之前发送 `Content-Type` 头。这会发送正确的 HTTP 头，以便浏览器知道加载 Shockwave Flash 插件。这导致了另一种可能发生的错误：输出除了 `Content-Type` 头之外的任何内容，例如空行。除了头和电影本身之外，输出其他内容会损坏文件，导致浏览器错误地显示该文件。此外，了解你希望最终输出看起来怎样的大致布局也是有帮助的。为了帮助布局使用 Ming 创建的 Flash 电影，你可以使用提供坐标系统的图形程序，或者直接使用坐标纸。

## SimpleXML

如今，XML 无处不在，因此有一种简单的方法来检索和解析这些文件是理所当然的。幸运的是，PHP 为我们提供了一个 XML 接口，用于利用 XML 数据，这是一个简单且易于使用的扩展：SimpleXML。SimpleXML 默认已安装，但如果你不打算使用它，建议在 `php.ini` 中将其禁用。需要注意的是，SimpleXML 也需要 PHP5。

顾名思义，该扩展的目的是在非常基本的级别访问 XML 文档。为了说明实现的简便性，创建一个包含海滨租赁信息的虚构 XML 文件（此文件将用于所有示例）：

```xml
<?xml version="1.0"?>

<rentals>

  <description>

    <name>The Bayfront</name>

    <type>condo</type>

    <view>oceanfront</view>

    <space>1200 square feet</space>

    <location>Wrightsville Beach</location>

    <price>1000 per week</price>

    <bed_bath>3 bedrooms, 2 bathrooms</bed_bath>

  </description>

  <description>

    <name>Paradise</name>

    <type>house</type>

    <view>oceanfront</view>

    <space>1000 square feet</space>

    <location>Wrightsville Beach</location>

    <price>900 per week</price>

    <bed_bath>2 bedrooms, 2 bathrooms</bed_bath>

  </description>

</rentals>
```

既然你有了 XML 文件，获取信息并将其放入对象中（使用 `simplexml_load_file()` 函数），以便你可以操作它：

```php
<?php

if (file_exists('beachfront.xml')) {

    $data = simplexml_load_file('beachfront.xml');

    print_r($data);

}

?>
```

你可以遍历该对象并以美观的方式显示结果（或者至少是更可读的格式）。向 `simple.php` 添加以下更改：

### 第 10 章

```php
<?php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');
    
    foreach($data as $main) {
        echo "<hr>";
        foreach ($main as $k => $v) {
            echo $k . ": " . $v . "<br />";
        }
    }
}
?>
```

除了 `simplexml_load_file()` 之外，还有许多与 SimpleXML 扩展配套的其他函数。`simplexml_load_string()` 将 XML 文档作为字符串加载。你首先必须将其内容分配给一个变量；然后你可以使用 `simplexml_load_string()` 函数将该变量的内容解析为你可用的对象。如果你希望操作对象，然后以 XML 文件的形式将其内容显示回浏览器，你可以使用 `$objectname->asXML()` 函数。如果你需要查看元素的属性或对象中任意节点的子节点，`attributes()` 和 `children()` 函数会很有帮助。如果你想从 DOM 文档中获取一个 DOM 节点并将其转换为 SimpleXMLElement 对象，`SimpleXML_import_dom()` 函数会很有用。

`xpath()` 函数允许你通过特定字符串在 XML 文档中进行搜索。它使用 W3C 的 XPath 来评估 XML 文档中的每个节点，之所以被称为“XPath”，是因为搜索关键字类似于文件的路径，因为每个元素同样都是嵌套的。如果你想更多地了解 XPath，请访问 W3C 关于该主题的文档：http://www.w3.org/TR/xpath。

如果你只想执行最简单的查询，这样就足够了，如下例所示：

```php
<?php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');
    
    //find and list all the "locations" in our XML file
    //"locations" are under "descriptions" which are under "rentals"
    $find = $data->xpath('/rentals/description/location');
    
    while (list(, $v) = each($find)) {
        echo $v . "\n";
    }
}
?>
```

此脚本将返回你 XML 文件中名为“location”节点的所有值。如果你想进一步深入查询，你就必须使用另一种方法。请记住，这是 SimpleXML，而不是 ComplexXML。

SimpleXML 提供了一种非常快速且直接的方式来访问简单的 XML 文档。它不提供太多的灵活性，而且只能处理最简单的 XML 文件。例如，如果你试图在包含 HTML 代码内容的 XML 文件上运行这些函数，将会遇到问题。除此之外，与目前可用的许多其他 XML/PHP 接口相比，它的使用要容易得多。

#### 总结

虽然本章仅涵盖了其中的一小部分，但仍有许多其他的 PHP 扩展可用。完整的列表可在 PHP 手册（http://www.php.net）中找到。你可能需要注意的一些扩展包括：

- `CURL`（客户端 URL 库函数）：允许你使用许多不同的协议（除 http 外，如 SSL、FTP 和 gopher）连接到页面。
- `DOM`：使用 DOM API 与 XML 文档交互，并随 PHP 默认安装捆绑提供。
- `SOAP`：利用 GNOME xml 库启用创建 SOAP 服务器和客户端。
- `ZIP` 扩展（Bzip2、rar、Zip、Zlib）：启用读取 zip 文件，每个扩展处理不同类型的压缩文件。

通过这种对 PHP 扩展的初步体验，我们希望你能够自信地探索 PHP 中那些鲜为人知但同样有用的函数。

## 11 AJAX

典型的 web 应用程序通过表单与用户交互。服务器向客户端发送表单，用户输入响应，表单被提交回服务器进行处理。表单处理完成后，服务器响应一个新的完整页面，其构成通常取决于用户上一次的表单提交。在与用户的每次交互中，都需要一个全新的页面。此类应用程序必须使用带宽，即使这些元素在以前的响应中已发送到客户端，它们仍会在每次页面请求时传输恒定的页面元素（例如站点导航）。此外，由于 web 应用程序在处理一次交互的结果以及新页面加载之前是无响应的，因此此类应用程序比桌面应用程序更慢。
