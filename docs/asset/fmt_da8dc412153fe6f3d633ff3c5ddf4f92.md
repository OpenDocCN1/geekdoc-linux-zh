
第一部分 `<packages></packages>` 保存了应用程序所需的所有扩展的列表。每个扩展通过 `<package />` 空标签指定，属性 `name=""` 指定扩展的名称。扩展的名称应与前文提到的 `get_loaded_extensions()` 返回的名称匹配。

第二部分包含定义特定应用程序设置（默认在 `php.ini` 中找到）和 PHP 自身版本要求的定义。每个 `<setting />` 标签可以对应一个 PHP 运行时配置设置。`name=""` 属性匹配配置设置的名称，`value=""` 属性保存将在 `php.ini` 中使用的任何值。`<php />` 标签允许你为应用程序指定版本要求——在 `minversion=""` 属性中指定最低版本，在相应的 `maxversion=""` 属性中指定最高版本（未显示）。

在 `reqs.xml` 的这个示例中，GD、MySQL 和 PostgreSQL 扩展被列为必需，允许的 PHP 最低版本为 5.0.0，并且 `register_globals` 指令必须设置为 off。

> **注意：** 在本示例中指定最低版本 5.0.0 在技术上是多余的——由于不同的对象模型，下面介绍的结构将仅在 PHP 5.0 及更高版本上运行。

### PHP 配置

配置检查器中的下一个文件是 `class.ConfigManager.php`，它充当脚本的中心控制点：

```php
<?php
class ConfigManager
{
    public $configfile = 'reqs.xml';
    public $configtype = 'xml';
    public $errors;
    
    public function __construct($configfile = null, $configtype = null)
    {
        if ($configfile)
        {
            $this->configfile = $configfile;
        }
        if ($configtype)
        {
            $this->configtype = $configtype;
        }
    }
    
    public function processConfig()
    {
        switch ($this->configtype)
        {
            case 'xml':
                require_once 'class.XMLConfigProcessor.php';
                $proc = new XMLConfigProcessor($this->configfile);
                $this->errors = $proc->process();
                break;
        }
        echo nl2br($this->errors);
    }
}
?>
```

这个类的第一部分应该相当直观。它通过声明类 `ConfigManager` 开始，并声明三个公共属性：

```php
<?php
class ConfigManager
{
    public $configfile = 'reqs.xml';
    public $configtype = 'xml';
    public $errors;
```

第一个属性 `configfile` 保存你将使用的配置文件的名称。该配置文件的默认值设置为 `reqs.xml`，因此，除非你使用不同的文件名，否则无需显式设置此属性。`configtype` 属性用于指定配置类型。在这种情况下，提供默认值 `xml` 以表示你的配置是 XML 格式。最后一个属性 `errors` 仅仅是后续处理过程中遇到的任何错误消息的占位符。

接下来是类的构造函数方法：

```php
public function __construct($configfile = null, $configtype = null)
{
    if ($configfile)
    {
        $this->configfile = $configfile;
    }
    if ($configtype)
    {
        $this->configtype = $configtype;
    }
}
```

虽然此构造函数中没有真正神奇的事情发生，但它确实允许在创建对象时传递配置文件和类型，并使用这些值设置相应的属性。

`ConfigManager` 中的最后一个方法是一切魔术发生的地方：

```php
public function processConfig()
{
    switch ($this->configtype)
    {
        case 'xml':
            require_once 'class.XMLConfigProcessor.php';
            $proc = new XMLConfigProcessor($this->configfile);
            $this->errors = $proc->process();
            break;
    }
    
    echo nl2br($this->errors);
}
```

`processConfig()` 方法首先确定配置类型，然后根据配置类型调用必要的代码并利用组件对象。目前，`processConfig` 中只指定了一种类型，即处理 XML 配置文件的类型。随着新配置处理器类型的创建，可以添加任意数量的额外情况。如果你希望在数据库中以存储配置，你可以设计自己的数据库配置处理对象，然后在此 `switch` 中添加一个情况，以调用新类中的任何处理方法。

请注意，`XMLConfigProcessor` 的类文件在此时引入，而不是在文件开头或类的更早位置引入。这样，只有当需要时才解析类文件，有助于减少如果使用不同配置类型时的额外处理。要使用 `XMLConfigProcessor`，只需实例化对象，将配置文件名传递给构造函数，最后调用处理配置的方法（将在本章后面详细介绍）。

这组文件中的下一个文件是一个简单的接口，用于定义任何配置处理类应支持的一组方法：

```php
<?php
interface ConfigProcessor
{
   public function checkExtensions();
   public function checkPHP();
   public function checkConfig();
   public function process();
}
?>
```

这个相当直观——这里定义的四个方法将规定任何配置类型的所有处理类的通用功能。前三个方法 `checkExtensions()`、`checkPHP()` 和 `checkConfig()` 主要用作实现类的内部方法，最后一个方法 `process()` 旨在作为触发其他三个方法的主要公共方法。

配置检查工具的最后一个文件是 `class.XMLConfigProcessor.php`，正如你可能从文件名猜到的，它处理 XML 配置文件：
