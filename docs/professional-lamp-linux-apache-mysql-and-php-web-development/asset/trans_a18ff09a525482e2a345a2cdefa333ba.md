

## PHP 配置

```php
$exts = $this->xml->xpath('/packages/package');
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

类名的开头相当普通——你包含接口文件，开始类，并定义一些属性。第一个属性 `XmlFile` 用于保存你的 XML 配置的**文件名**。第二个属性 `Message` 将用于捕获在处理文件时创建的任何错误消息。第三个也是最后一个属性 `Xml`，将保存一个由 PHP 的 SimpleXML 扩展创建的 XML 对象。在属性定义之后是一个简单的构造函数，如果在实例化期间传递了**文件名**，它会设置 `xmlFile` 的值：

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

    public function process()
    {
        // Check for needed libraries
        if (!$this->checkDeps() or
            !$this->checkConfigAccess())
        {
            return $this->message;
        }

        $this->xml = simplexml_load_file($this->xmlfile);

        if (!$this->checkPHP() or
            $this->checkExtensions() or
            !$this->checkConfig())
        {
            return $this->message;
        }
    }
```

构造函数之后的 `process()` 方法是从类外部调用的主方法。它包含了对类中所有其他组件方法的调用，这些方法检查 XML 配置文件中的各个要求和部分。

在 `process()` 的第一部分中，你会检查配置文件是否可访问，以及 PHP 安装是否具备该类正常运行的所有必要条件。如果其中任何一个检查失败，该方法应该终止并返回遇到的任何错误消息。

接下来，SimpleXML 扩展用于将配置文件的内容加载到一个 XML 对象中，准确地说是一个 `simplexml_element` 对象。这个 `simplexml_object` 可用于轻松遍历 XML 并根据需要提取标签和属性。

最后，`process()` 调用了来自 `ConfigProcessor` 接口的其余三个方法，以检查 PHP 版本、可用的扩展和配置设置。

你接下来遇到的方法是 `checkConfigAccess()`。此方法用于检查 XML 配置文件是否实际存在于文件系统上，如果存在，则进一步检查它是否可读。如果文件不存在或不可读，则向 `message` 属性添加一条错误消息。请注意，在方法的末尾调用了 `clearstatcache()`。`file_exists()` 和 `is_readable()` 的结果会被 PHP 缓存，因此在完成工作后清除结果缓存是个好主意，以防止后续出现错误的结果：

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

接下来是 `checkDeps()`。顾名思义，此方法检查类本身的依赖项。对于 `XMLConfigProcessor` 来说，唯一非标准的 PHP 要求是 SimpleXML 扩展的可用性。例如，如果你后来决定修改此类以使用 XML Parser 函数或 DOM XML 扩展，你需要在此方法中添加相应的检查。

为了检查 SimpleXML，你只需使用本章前面介绍的 `extension_loaded()` 函数即可。如果 SimpleXML 不可用，则将另一条错误消息添加到消息堆中：

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

现在该动手处理一下你的 XML 配置文件了。在 `checkExtensions()` 中，你需要做的第一件事是收集配置文件中列出的所有扩展。如前所述，每个包都在外层 `<packages></packages>` 标签中作为一个 `<package />` 标签列出。要获取所有这些包的列表，你需要使用 SimpleXML 的 `xpath()` 方法：

```php
public function checkExtensions()
{
    $returnValue = true;

    // Check for all listed extensions
    $exts = $this->xml->xpath('/packages/package');

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
}
```

`xpath()` 方法接收一个表示元素在文档层级中位置（即 Xpath 路径）的字符串，并返回一个 `simplexml_element` 对象的数组——在这种情况下，每个对象代表一个单独的 `<package />` 标签。

一旦你有了包标签的数组，你只需遍历它们，检查每个包是否可用。由于包名称存储在每个 `<package />` 标签的 `name=" "` 属性中，你可以使用方括号语法和字符串作为键，类似于数组键的方式访问其值。再次使用 `extension_loaded()` 函数来检查每个包，如果不可用，则向消息堆中添加一条错误消息。

从 `ConfigProcessor` 实现的下一个方法是 `checkPHP()`。此方法检查 PHP 本身的版本，以查看应用程序是否可以在该版本上运行。在方法开始时，你首先再次使用 `xpath()` SimpleXML 方法，以检查配置文件中是否存在 PHP 版本要求：

```php
public function checkPHP()
{
    // Check if PHP requirement is present
    if (count($phpreq = $this->xml->xpath('/environment/php')) == 0)
    {
        return true;
    }

    // Flatten element array
    $phpreq = $phpreq[0];

    // Check minimum version
    if ($phpreq['minversion'] and
        version_compare(PHP_VERSION,
                       $phpreq['minversion']) < 0)
    {
        $this->message .= "Warning: " .
                          "PHP version is less than " .
                          $phpreq['minversion'] . "\n";
        return false;
    }

    // Check maximum version
    if ($phpreq['maxversion'] and
        version_compare(PHP_VERSION,
                       $phpreq['maxversion']) > 0)
    {
        $this->message .= "Warning: " .
                          "PHP version is greater than " .
                          $phpreq['maxversion'] . "\n";
        return false;
    }

    return true;
}

public function checkConfig()
{
    $returnValue = true;

    // Get all config values
    $cfg = ini_get_all();

    // Cycle through setting elements
    $settings = $this->xml->xpath('environment/setting');
    foreach ($settings as $setting) {
        $value = $setting['value'];
        // Convert boolean values to ini_get() values
        switch (strtolower($value)) {
            case 'off':
            case '0':
            case 'false':
            case 'no':
                $value = '';
                break;
            case 'on':
            case 'true':
            case 'yes':
                $value = '1';
                break;
        }

        // Flatten name
        $name = (string) $setting['name'];

        // Check config value, set if needed
        if (!array_key_exists($name, $cfg) or
            ($value !=
               $cfg[$name]['local_value']) and
            ini_set($name, $setting['value']) === false)) {
            $returnValue = false;
            $this->message .= "Warning: " .
                              "not set to the required value of: "
                              . $name .
                              . $setting['value'] . ".\n";
        }
    }

    return $returnValue;
}
```

