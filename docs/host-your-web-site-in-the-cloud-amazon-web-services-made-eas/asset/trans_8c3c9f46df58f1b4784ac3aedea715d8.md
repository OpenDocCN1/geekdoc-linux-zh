
## 第 11 章

## 综合应用：CloudList

在本章中，我们将使用 Amazon EC2 基础设施、S3 和 SimpleDB 创建一个分类广告应用程序，我将其命名为 CloudList。本章的各个部分反映了我的开发过程，因此你应该能看到我是如何组装这个应用程序的。

### 设计应用程序

我们的项目是创建一个简单的分类广告应用程序。该应用程序将允许多个城市的用户提交和查看分类广告。

我们需要跟踪以下类型的数据：

- 地点——城市列表和州列表
- 类别——分类广告类别列表
- 物品——分类广告列表

我们将为每个广告存储以下字段：

- 城市
- 州
- 日期
- 价格
- 类别
- 标题
- 描述
- 图片（全尺寸和缩略图）

由于每个 SimpleDB 属性值限制为 1,024 字节，因此我们将描述、图片和缩略图存储在 S3 中。为了追求简洁，我们将避免包含任何联系信息（电子邮件地址或电话号码），但你可以自由扩展该应用程序。

每种数据都需要自己的 SimpleDB 域，因此让我们选择一些好听的名称：

```php
// cloudlist/include/cloudfunctions.inc.php (摘录)

define('CL_CITY_DOMAIN', 'cl_cities');
define('CL_CAT_DOMAIN', 'cl_categories');
define('CL_ITEM_DOMAIN', 'cl_items');
```

我们将把这些常量定义放在公共文件 **cloudfunctions.inc.php** 中，以便在所有 CloudList 应用程序文件中包含它。此时，我们尚未对应用程序的外观或行为做出任何决定，但这些考虑不会影响数据模型。

### 实用函数和程序

下一步是创建一些命令行实用程序，用于用初始数据填充 SimpleDB 域。

为了创建我们要使用的 SimpleDB 域，我们可以简单地修改第 8 章中的 *create_domain.php* 脚本：

```php
// cloudlist/create_domain.php (摘录)
...
$Sdb = new AmazonSDB();

foreach (array(CL_CITY_DOMAIN,
               CL_CAT_DOMAIN,
               CL_ITEM_DOMAIN) as $domain)
{
    $Res = $Sdb->create_domain($domain);
    if (!$Res->isOk())
    {
        exit("Create domain operation failed for domain ${domain}\n");
    }
    print("Domain ${domain} created.\n");
}
...
```

下面是一个添加新城市——实际上是城市/州对——的脚本：

```php
// cloudlist/add_city.php (摘录)
#!/usr/bin/php
<?php
error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/cloudfunctions.inc.php');

if ($argc < 3)
{
    exit("Usage: " . $argv[0] . " CITY STATE\n");
}

$city  = $argv[1];
$state = $argv[2];

$key  = $state . '_' . $city;
$sattrs = array('City' => $city,
                'State'  => $state);

$Sdb = new AmazonSDB();

$sres = $Sdb->put_attributes(CL_CITY_DOMAIN, $key, $sattrs, true);

if ($sres->isOk())
{
    print("Added city ${city} in ${state}\n");
}
else
{
    $error = $sres->body->Errors->Error->Message;
    print("Could not add city: ${error}\n");
}
?>
```

我们还将需要一个脚本来添加一个或多个类别的列表：

```php
// cloudlist/add_category.php (摘录)
#!/usr/bin/php
<?php

error_reporting(E_ALL);

require_once('cloudfusion.class.php');
require_once('include/cloudfunctions.inc.php');

if ($argc < 2)
{
    exit("Usage: " . $argv[0] . " CATEGORY ...\n");
}

$sdb = new AmazonSDB();

for ($i = 1; $i < $argc; $i++)
{
    $category = $argv[$i];

    $Key = $category;
    $attrs = array('Category' => $category);

    $res = $sdb->put_attributes(CL_CAT_DOMAIN, $Key, $attrs, true);

    if ($res->isOk())
    {
        print("Added category ${category}\n");
    }
    else
    {
        $error = $res->body->Errors->Error->Message;
        print("Could not add category: ${error}\n");
    }
}
?>
```

现在，我们可以使用这些命令行脚本来设置一些示例数据。首先，我们设置域：

```bash
$ create_domain.php
Domain cl_cities created.
Domain cl_categories created.
Domain cl_items created.
```

然后，我们添加一些城市：

```bash
$ php add_city.php Bethesda MD
Added city Bethesda in MD
$ php add_city.php Redmond WA
Added city Redmond in WA
$ php add_city.php Boise ID
Added city Boise in ID
$ php add_city.php "San Francisco" CA
Added city San Francisco in CA
```

接下来，我们添加类别：

```bash
$ php add_category.php Cars Trucks Homes Furniture
Added category Cars
Added category Trucks
Added category Homes
Added category Furniture
```

如果你还记得第 8 章的内容，对 SimpleDB 的 `select` 方法的每次调用最多可以返回 2,500 条结果，具体取决于返回的属性大小和数量。然而，我们很可能需要运行可能会产生长结果列表的 SimpleDB 查询。因此，让我们创建一个函数，以便更轻松地捕获和处理任意大小的结果集。以下是 `runQuery` 函数的代码：

```php
// cloudlist/include/cloudfunctions.inc.php (摘录)

function runQuery($sdb, $query)
{
    $next = '';
    $results = array();

    do
    {
        $res = $sdb->select($query, array('NextToken' => $next));
        if (!$res->isOk())
        {
            return null;
        }

        $next = isset($res->body->SelectResult->NextToken) ?
               (string) $res->body->SelectResult->NextToken
               : '';

        foreach ($res->body->SelectResult->Item as $item)
        {
            $attributes = array();
            foreach ($item->Attribute as $attribute)
            {
                $attributes[(string) $attribute->Name] =
                       (string) $attribute->Value;
            }

            $Key = (string) $item->Name;
            $results[$Key] = $attributes;
        }
    } while ($next != '');

    return $results;
}
```

该函数接受一个作为字符串的 SimpleDB 查询，进行一系列对 **select** 方法的调用以检索所有结果，然后返回一个包含所有结果的 PHP 关联数组。然后我们可以围绕此函数编写一些非常简单的包装器，以返回所有城市和类别的数组：

```php
// cloudlist/include/cloudfunctions.inc.php (摘录)

function getCities($Sdb)
{
    $query = "select * from " . CL_CITY_DOMAIN;
    return runQuery($Sdb, $query);
}

function getCategories($Sdb)
{
    $query = "select * from " . CL_CAT_DOMAIN;
    return runQuery($Sdb, $query);
}
```

**getCities** 函数返回城市数据，格式如下：

```text
Array
(
    [WA_Seattle] => Array
    (
        [State] => WA
        [City] => Seattle
    )
    [WA_Redmond] => Array
    (
        [State] => WA
        [City] => Redmond
    )
    ...
)
```

当然，添加新的分类列表比城市和类别稍微复杂一些。能够这样做从命令行或 Web 表单中是非常有用的。因此，我们将创建一个单一的（如果有点复杂）函数，名为 **addCloudListItem**，用于添加新项，该函数可以从命令行或网页脚本中调用。

在 **addCloudListItem** 函数中，我们将使用我们在第 4 章中的 **thumbnailImage** 函数。请确保将该函数复制到 **cloudfunctions.inc.php** 文件中。**thumbnailImage** 函数还使用 THUMB_NAIL 常量中的值来确定缩略图的大小，因此我们还需要将其添加到我们的 **cloudfunctions.inc.php** 文件中：

```php
// cloudlist/include/cloudfunctions.inc.php (摘录)
define( 'THUMB_SIZE', 200 );
```

我们还将重用第 4 章中的 uploadObject 函数，将图像文件上传到我们的 S3 桶，因此也将该函数复制到 cloudfunctions.inc.php 文件中。

让我们分解 addCloudListItem 代码并逐步检查。它是这样开始的：

```php
// cloudlist/include/cloudfunctions.inc.php (摘录)

function addCloudListItem($sdb, $s3, $city, $state, $date,
                         $price, $category, $title, $description,
                         $imagePath)
{
```

由于数据将用于 SimpleDB，我们需要一个唯一的键。让我们取一些字段，将它们组合成一个字符串，然后计算该字符串的 MD5 哈希值，如下所示：

```php
// cloudlist/include/cloudfunctions.inc.php (摘录)
$Key = md5($city . $state . $date . $price . $category . $title);
```

下一步（这是一个很大的步骤）是处理与列表相关的图像。函数的 $imagePath 参数可以是远程图像的 URL，也可以是本地图像的完整限定路径名。这是通过 PHP 函数 file_get_contents 实现的。如果没有与列表相关的图像，我们将为该参数传递 null。以下是我们需要下载图像、创建缩略图版本并将两个图像都存储在 S3 中的代码：

```php
// cloudlist/include/cloudfunctions.inc.php (摘录)

if ($imagePath !== null)
{
    $imageIn  = file_get_contents($imagePath);
    $imageMem = ImageCreateFromString($imageIn);

    $fileOut = tempnam("/tmp", "_aws") . ".aws";
    $ret     = ImageJPEG($imageMem, $fileOut, 100);
    $imageOut = file_get_contents($fileOut);
```
