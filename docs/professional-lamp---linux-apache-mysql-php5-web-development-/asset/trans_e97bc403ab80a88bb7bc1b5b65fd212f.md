

## 第 10 章

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

## 总结

虽然本章仅涵盖了其中的一小部分，但仍有许多其他的 PHP 扩展可用。完整的列表可在 PHP 手册（http://www.php.net）中找到。你可能需要注意的一些扩展包括：

- **CURL（客户端 URL 库函数）**：允许你使用许多不同的协议（除 http 外，如 SSL、FTP 和 gopher）连接到页面。
- **DOM**：使用 DOM API 与 XML 文档交互，并随 PHP 默认安装捆绑提供。
- **SOAP**：利用 GNOME xml 库启用创建 SOAP 服务器和客户端。
- **ZIP 扩展（Bzip2、rar、Zip、Zlib）**：启用读取 zip 文件，每个扩展处理不同类型的压缩文件。

通过这种对 PHP 扩展的初步体验，我们希望你能够自信地探索 PHP 中那些鲜为人知但同样有用的函数。

## 11 AJAX

典型的 web 应用程序通过表单与用户交互。服务器向客户端发送表单，用户输入响应，表单被提交回服务器进行处理。表单处理完成后，服务器响应一个新的完整页面，其构成通常取决于用户上一次的表单提交。在与用户的每次交互中，都需要一个全新的页面。此类应用程序必须使用带宽，即使这些元素在以前的响应中已发送到客户端，它们仍会在每次页面请求时传输恒定的页面元素（例如站点导航）。此外，由于 web 应用程序在处理一次交互的结果以及新页面加载之前是无响应的，因此此类应用程序比桌面应用程序更慢。

AJAX（异步 JavaScript 和 XML）指的是一组技术，允许创建富客户端 web 应用程序，其中应用程序处理的大量责任被交给客户端。具体来说，AJAX 应用程序通常使用 XHTML 和 CSS 进行语义标记和展示，使用 XML 来格式化将在客户端和服务器之间交换的数据，并使用 JavaScript 与服务器通信并操作文档对象模型（DOM）。使用 AJAX 时，客户端和服务器之间的通信可以仅限于数据，因为客户端具有处理展示和用户交互所需的必要功能。此外，这种通信是异步进行的，且无需刷新页面。这使得应用程序的客户端部分即使在数据与服务器交换期间也能保持响应。如果用户执行了一个需要向服务器发送请求的操作，请求可以发送，并且应用程序在等待响应期间（甚至发出更多请求时）可以处理进一步的交互。这一概念如图 11.1 所示。

当今最流行的 AJAX 应用程序可能是 Google 的 [GMail](http://www.gmail.com)，它是一个基于 web 的电子邮件框架。在传统基于 web 的电子邮件客户端中，用户的几乎每个操作都会导致整个页面或框架的刷新。由于 GMail 采用了 AJAX，页面从不刷新。相反，界面通过基于用户与应用程序的交互以及与 GMail 服务器的 XML 通信，利用 JavaScript 操作 DOM 进行动态更新。这使得用户例如可以撰写电子邮件，点击发送，并在 GMail 服务器处理实际发送消息的同时继续阅读他的或她的电子邮件。在阅读其余邮件时，他或她将收到一条状态消息，表明消息已成功发送。

![](img/cacdd24f2926f10ee3219256ad732604_299_0.png)

## 历史

AJAX 本身并不新鲜；其背后的思想也是。事实上，过去已经开发和使用了多种无需刷新页面即可与服务器通信的方法。

## 图像源技巧

JavaScript 允许使用 Image 对象动态加载图像。当创建一个图像并设置其 src 属性时，浏览器会发送对该图像的请求，并尝试将响应打包在图像对象中。开发人员已利用这一点通过设置 src 属性为服务器端脚本的 URI，并在查询字符串中向服务器传递数据，从而与服务器进行单向通信。服务器端脚本随后可能会更新数据存储。通常响应中不会返回图像，但这不会造成问题，因为开发人员并不将 Image 对象用于其预期目的。

这种技术的优点包括：

- 它允许在不刷新的情况下向服务器发送数据。
- 它可以读取对象属性以确定请求何时完成。

然而，它也有一些缺点：

- 它无法从服务器接收非图形数据（通信是单向的）。
- 它无法检测或处理在尝试通信期间可能发生的 HTTP 错误。

## 隐藏框架

许多开发人员发现图像源技巧不足以满足需求，并且除了向服务器发送数据外，还需要从服务器接收信息的能力。此时，使用隐藏框架的技术应运而生。在此技术中，开发人员使用一个不可见的框架（根据框架集设置，通过将高度或宽度设为 0）作为载体。隐藏框架只是一个包含最少 HTML 元素集合加一个 script 元素的页面。该 script 元素通常仅仅是数组和变量的定义，其值由服务器写入。因此，控制框架（可见的那个）可以将此框架的 location 属性设置为服务器端脚本的地址，可选地通过查询字符串向其发送数据。然后浏览器发出此请求。服务器端脚本处理查询字符串中传递的任何信息，然后以有效的 JavaScript 语法写入数据。查看以下代码以了解大致思路。

```html
<?php
$suname = $_GET['username'];
?>
<script type="text/javascript">
top.usernameOK = <?php echo isUsernameAvailable($suname); ?>;
top.usernameAlts = new Array(<?php echo implode(',', getSimilarNames($suname)); ?>);
top.frames[1].readVars();
</script>
```

> 此代码位于隐藏通信框架中。在此代码示例中，写入一个布尔值以指示通过查询字符串传递给脚本的用户名的可用性。当浏览器的 JavaScript 引擎执行此脚本时，它将把该布尔值存储在名为 usernameOK 的 JavaScript 变量中。

