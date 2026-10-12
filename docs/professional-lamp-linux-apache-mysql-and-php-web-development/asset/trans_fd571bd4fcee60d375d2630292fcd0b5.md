
# 更冷门的 PHP

```php
$tile_northing+=250)
for($tile_easting=$leftmost_tile_easting;
$tile_easting<=$rightmost_tile_easting;
$tile_easting+=250)
{
$full_image_x = 100*($tile_easting-$minimum_easting)/250;
$full_image_y = 100*($maximum_northing-$tile_northing)/250;
$tile_name = sprintf('%07d%07d.png', $tile_northing, $tile_easting);
if(!file_exists('tiles/'.$tile_name)) continue;
$tile = imagecreatefrompng('tiles/'.$tile_name);
imagecopy($full_image, $tile, $full_image_x, $full_image_y, 0, 0, 100, 100);
imagedestroy($tile);
}
ob_start();
imagepng($full_image);
imagedestroy($full_image);
$this->png_data = ob_get_contents();
ob_end_clean();
$this->data_length = strlen($this->png_data);
return true;
}

function stream_close()
{
$this->png_data = null;
}

function stream_read($bytes)
{
if(strlen($this->png_data)==0)
return false;
$return = substr($this->png_data, 0, $bytes);
$this->png_data = substr($this->png_data, $bytes);
return $return;
}

function stream_write(){}
function stream_eof()
{
return $this->png_data == 0;
}

function stream_tell()
{
return $this->data_length-strlen($this->png_data);
}

function stream_seek()
{
return false;
}

function stream_flush(){
    return false; // We don't store data, silly.
}

function stream_stat() 
{ 
    return false; 
} 

// We put the stream wrapper registration here, with the wrapper it 
// registers, to save the hassle of remembering to register it every 
// time we include the file. 
// 
// This of course assumes that we're never tempted to use the same 
// wrapper protocol (nzmg) for different types of stream. 
stream_wrapper_register('nzmg', 'orthophoto_stream');
```

## 第 3 章

正如代码最后一行所示，该类被注册为“nzmg”协议。此处实现的 nzmg URL 的完整格式为 nzmg:///nnnnnnneeeeeeeerrrrrrr，其中七位数字分别指定北向坐标（对于奥克兰而言，是 6460000 到 6489750 之间的某个米数）、东向坐标（2650000 到 2689750 之间的米数）以及半径（同样以米为单位，虽然要求超过 20000 米的半径几乎没有意义，因为那是整个 16 × 12 公里图像的斜边长度）。

之所以使用“北向坐标”和“东向坐标”而不是经纬度来表示位置，是因为地球既不是一个完美的球体，甚至也不是一个特别对称的椭球体，因此二者之间的转换绝非易事。本示例中采用的新西兰地图网格（New Zealand Map Grid）是通过经验确定的，由此产生的经纬度与北向/东向坐标的映射涉及诸如求值六度复杂多项式等操作。（土地测量官办公室发布的精确规范可作为 OGS 技术报告 4.1 获取，并可在 LINZ 网站上下载。）这与本示例的目标无关，就像将地标和投递地址映射到坐标这一练习一样无关。同样，输入数据验证的问题（包括将半径限制在比 20 公里更合理的范围内）也与此无关。所有此类具体任务都应在达到此阶段之前处理，每一项都应尽可能具有广泛的适用性。

图像存储为一系列 PNG 文件，每个文件尺寸为 100 × 100 像素，对应现实世界中的 250 × 250 米，因此总共有 19,200 个这样的文件。每个文件的命名根据其西南角（左下角）的北向坐标和东向坐标。北向坐标向上增加，东向坐标向右增加。由于北向坐标和东向坐标本身以米为单位测量（这就是它们的用途），位于 647000202660000.png 正北方的瓦片将是 64702502660000.png，而位于正东方的瓦片将是 6470002660250.png。这些瓦片的位置安排使得它们已知的北向坐标和东向坐标都是 250 的倍数。由于父图像也具有此属性，且其尺寸也是 100 像素的倍数，因此这些瓦片精确覆盖了父图像。

同样，大部分工作都在 `stream_open()` 中完成，它确定请求图像的大小、其左下角像素所在的瓦片，以及垂直和水平方向需要的瓦片数量。使用 GD 库创建一个新图像（由于图像是灰度的，因此没有必要使用 truetype），尺寸为此处所需的尺寸，然后通过一对嵌套循环从磁盘读取适当的瓦片，并将它们复制到正在进行的图像中。在任何时间点，用于存储图像数据的总内存量足以容纳进行中的图像和一个 100 × 100 像素的瓦片。

`stream_open()` 的最后一步是将组装好的 GD 库图像转换为 PNG 数据。这是通过一种简单的方法实现的：要求 GD 库将图像输出为 PNG，并使用输出缓冲来捕获结果。

每次调用 `stream_read()` 都会返回另一块 PNG 数据，并丢弃已经返回的部分。

由于这是一个由实时生成数据组成的只读流，因此剩余的大部分流访问方法都没有意义。关于数据可以说的一点是还剩多少可读内容，这使得可以定义 `stream_tell()`。

使用该类的代码无需了解它是如何将 `nmgz://` 请求与响应匹配的。就它关心的而言，`nmgz://648208926677120000500` 只是另一个文件，恰好包含奥克兰中心区 1 公里宽快照的 PNG 图像。

但请等一下。如果它只是 PNG 数据，而且只是一个文件，那么从各方面来看，*它只是一个 PNG 文件*。确实如此。下面是使用此封装器的一个示例。假设该类位于其自己的 `orthophoto_stream.php` 文件中，并且假设经纬度已转换为北向坐标和东向坐标，并且半径不会太大或太小。

```php
include_once('orthophoto_stream.php'); // 当然，在使用之前必须声明该类。
function display_orthophoto($northing, $seasting, $radius)
{
  $filename = sprintf('nmgz://%07d%07d', $northing, $seasting, $radius);

  // 所有基于流的操作都在这里发生。
  $image = imagecreatefrompng($filename);

  // 一点后处理，以使代码超越琐碎。
  // 绘制一个指定半径的圆（图像毕竟是方形的），并在中心放置一个十字。
  // 我们需要找到图像的白色值
  $white = imagecolorsearch($image, 255, 255, 255);
  if($white==-1) // 好的，它之前不存在。
    $white = imagecolorallocate($image, 255, 255, 255);
  // 圆以图像中心为圆心，且大小刚好足以
  // 触及边缘。
  $imagesize = imageX($image);
  $middle = $imagesize>>1;
  imageellipse($image, $middle, $middle, $imagesize, $imagesize, $white);
  imageline($image, $middle, $middle+5, $middle, $middle-5, $white);
  imageline($image, $middle+5, $middle, $middle-5, $middle, $white);
  imagestring($image, 0, 0, 0, 0,
              'Sourced from Orthophoto R11 Auckland Crown Copyright Reserved.',
              $white);
  imagepng($image);
  imagedestroy($image);
}
```

不用说，这个示例是在实际用途和教学用途之间达成的妥协，`orthophoto_stream` 类在很多方面都有改进的空间。

其中一个方面是，提供的 21 位数字文件名可以附加一个扩展名来指示所需的图像格式，而不是固定生成 PNG。其他方面包括更现实（或至少更灵活）的存储机制，用户可以通过更完善的 URL（包括主机名和路径）来控制。还要考虑将部分耗时工作移至 `stream_read()` 中的可能性，从而减少任何给定时间需要保留的图像数据量。（但请注意，由于 GD 库只缓冲完整图像，你将需要编写自己的代码来输出图像数据，这些数据在等待未来输入以完成之前是正确但不完整的。）

如果你遵循 RFC 3986 中定义的流资源命名 URL 系统，并参考 RFC 2718 中的指南，你会对自己很有帮助。事实上，可能已经存在一个与你应用程序相匹配的命名方案。（官方注册表由互联网号码分配机构维护，位于 http://www.iana.org/assignments/uri-schemes）。如果存在，请使用它。这样，你的应用程序将来可以与使用相同方案的其他应用程序协作，而无需额外的 URL 转换层将它们粘合在一起。（实际上，对于任何数据格式或通信协议也是如此——如果世界其他地方已经拥有你想要的标准，就使用它，节省自己创建新标准的时间和精力。）

> 请注意，所有 PHP URL 都要求在协议名称后使用 ://，无论是否涉及命名权威（主机），因为 PHP 使用该字符序列来区分 URL 和本地文件路径。用 RFC 3986 的术语来说，PHP 仅实现“hier-part”组件给出的四个产生式中的第一个，并将“naming-authority”组件设为可选。符合 RFC 的变通方法是使用 :///，隐含指定本地主机作为命名权威。

## 总结

这是对 PHP 原生函数集中一些较为冷门区域的简要介绍。通过利用这些功能，你的代码可以在不牺牲可读性的情况下变得更加紧凑和可靠。数组函数通常可以替代有时复杂的循环，将任务简化为一行代码和一个可以捕获并存储在库中以便重用的辅助函数。函数处理函数允许你在运行时不仅决定你想使用哪个函数（switch 语句可以做到这一点），还可以决定你希望从这个列表中选择的函数，甚至从头创建函数。流允许你隐藏外部数据读取或写入的实现细节，允许程序的其余部分将其视为另一个文件。

PHP 始终在添加新功能——用于微调其操作的新的初始化设置、增强现有功能实用性的新参数（即使是久负盛名的函数 str_replace() 在 PHP5 中也被赋予了新参数）、新函数，甚至全新的函数类别。所有这些使得学习 PHP 成为一项持续的过程，总有一些你尚未了解的东西。

