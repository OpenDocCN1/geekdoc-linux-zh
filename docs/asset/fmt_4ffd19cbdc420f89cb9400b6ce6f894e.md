
类的开头相当正常——包含接口文件，开始类，并定义一些属性。第一个属性 `$xmlFile` 用于保存 XML 配置文件的文件名。第二个属性 `$message` 将用于捕获在处理文件时生成的任何错误消息。第三个也是最后一个属性 `$xml` 将保存由 PHP 的 SimpleXML 扩展创建的 XML 对象。在属性定义之后，是一个简单的构造函数，如果在实例化时传入了文件名，它会设置 `xmlFile` 的值：

```php
<?php

require_once 'interface.ConfigProcessor.php';

class XMLConfigProcessor implements ConfigProcessor
{

    public $xmlfile;
    private $message = '';
    private $xml;

    public function __construct($xmlfile = null)
    {
        if ($xmlfile)
        {
            $this->xmlfile = $xmlfile;
        }
    }
```

紧跟在构造函数之后的 `process()` 方法是从类外部调用的主要方法。它包含了对类中所有其他组件方法的调用，这些方法用于检查 XML 配置文件中的各个要求和部分。

在 `process()` 的第一部分，你检查配置文件是否可访问，以及 PHP 安装是否具备此类正常运作所需的一切条件：

```php
public function process()
{
    // Check for needed libraries
    if (!$this->checkDeps() or
        !$this->checkConfigAccess())
    {
        return $this->message;
    }
```

如果这些检查中任何一个失败，该方法应终止并返回遇到的任何错误消息。

接下来，使用 SimpleXML 扩展将配置文件的内容加载到一个 XML 对象中，确切地说是一个 `simplexml_element` 对象。这个 `simplexml_object` 可以用于轻松遍历 XML 并在需要时提取标签和属性：

```php
$this->xml = simplexml_load_file($this->xmlfile);
```

最后，`process()` 调用了 `ConfigProcessor` 接口的其余三个方法，以检查 PHP 版本、可用扩展和配置设置：

```php
if (!$this->checkPHP() or
    !$this->checkExtensions() or
    !$this->checkConfig())
{
    return $this->message;
}
```

下一个遇到的方法是 `checkConfigAccess()`。该方法检查 XML 配置文件是否实际存在于文件系统中，如果存在，则进一步检查其是否可读。如果文件不存在或不可读，则会向 `message` 属性添加一条错误消息。请注意，在方法末尾调用了 `clearstatcache()`。PHP 会缓存 `file_exists()` 和 `is_readable()` 的结果，因此，完成后清除结果缓存是个好主意，以防止后续出现异常结果：

```php
private function checkConfigAccess()
{
    $returnValue = false;

    // Check to see if config file exists and is readable
    if (file_exists($this->xmlfile) and
        is_readable($this->xmlfile))
    {
        $returnValue = true;
    }
    else
    {
        $this->message .= "Warning: " .
                          "Could not access config file.\n";
    }

    // Clear cached filesystem lookups
    clearstatcache();

    return $returnValue;
}
```

接下来是 `checkDeps()`。顾名思义，该方法检查类本身的依赖项。对于 `XMLConfigProcessor`，唯一的非标准 PHP 要求是 SimpleXML 扩展的可用性。如果你之后决定修改此类以使用 XML 解析器函数或 DOM XML 扩展（例如），你会需要向该方法添加相应的检查。

要检查 SimpleXML，你只需使用本章前面介绍过的 `extension_loaded()` 函数。如果 SimpleXML 不可用，则向错误消息堆栈中添加另一条错误消息：

```php
private function checkDeps()
{
    $returnValue = true;

    // Check for SimpleXML
    if (!extension_loaded('SimpleXML'))
    {
        $returnValue = false;
        $this->message .= "Warning: " .
                          "SimpleXML extension not available.\n";
    }

    return $returnValue;
}
```

现在，是时候动手整理一下你的 XML 配置文件了。在 `checkExtensions()` 中，你需要做的第一件事是收集配置文件中列出的所有扩展。如前所述，每个包都作为 `<package />` 标签列出，并包含在一组外围的 `<packages></packages>` 标签内。要获取所有这些包的列表，你使用 SimpleXML 的 `xpath()` 方法：

```php
public function checkExtensions()
{
    $returnValue = true;

    // Check for all listed extensions
    $exts = $this->xml->xpath('/packages/package');
```

`xpath()` 方法接受一个表示元素在文档层次结构中的位置（其 Xpath 路径）的字符串，并返回一个 `simplexml_element` 对象数组——在本例中，每个对象代表一个单独的 `<package />` 标签。

一旦你拥有了包标签的数组，只需遍历它们，检查每一个是否可用。由于包名存储在每个 `<package />` 标签的 `name=""` 属性中，你可以使用括号语法和内部的字符串，像访问数组键值一样来访问这些值。再次使用 `extension_loaded()` 函数来检查每个包，如果不可用，则向错误消息堆栈中添加一条消息：

```php
foreach ($exts as $ext)
{
    if (!extension_loaded($ext['name']))
    {
        $returnValue = false;
        $this->message .= "Warning: " .
            $ext['name'] .
            " extension not available.\n";
    }
}

return $returnValue;
```

下一个来自 `ConfigProcessor` 接口的实现方法是 `checkPHP()`。该方法检查 PHP 本身的版本，以确定应用程序是否可以在该版本上运行。在方法开始时，你首先使用 SimpleXML 的 `xpath()` 方法再次检查配置文件中是否存在 PHP 版本要求：

```php
public function checkPHP()
{
    // Check if PHP requirement is present
    if (count($phpreq = $this->xml->xpath('/environment/php')) == 0)
    {
        return true;
    }
```

# 第 5 章

如果发现 PHP 版本要求，然后将 `xpath()` 返回的 `simplexml_elements` 数组替换为数组中的第一个（也是希望唯一的）对象：

```php
// 扁平化元素数组
$phpreq = $phpreq[0];
```
