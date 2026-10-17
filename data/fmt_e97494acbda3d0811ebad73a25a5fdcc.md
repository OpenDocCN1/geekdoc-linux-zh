
# 正射影像流示例

```php
<?php
/*
** 正射影像流使用由新西兰土地信息局维护的正射影像数据集。
** phototest 遵循 `Topographic Map 260` 系列；使用的坐标是新西兰地图格网
** (NZMG) 的坐标，这是一个该国独有的系统。
**
** 航拍照片的分辨率为每像素 2.5 米，精度为 ±12.5 米。
*/

class orthophoto_stream
{
    // 这是将由流反馈回来的生成的 PNG 数据。
    private $png_data;

    // 用于 feof() 函数 / stream_tell() 方法。
    private $data_length;

    function stream_open($path, $mode, &$options, &$opened_path)
    {
        // 这是一个只读流
        if(preg_match('/^w+a$/', $options)) return false;
        $path = parse_url($path);
        $coordinates = $path['host']; // 在这里找到它很荒谬，但参见
                                      // 该章节末尾的注释。
        if(strlen($coordinates)!=21) return false;
        if(strspn($coordinates, '0123456789')==21) return false;
        list($nothing, $easting, $radius)=sscanf($coordinates, '%07d%07d%07d');

        $full_image_size = ceil($radius*2*100/250);
        $full_image = imagecreate($full_image_size, $full_image_size);
        $black = imagecolorallocate($full_image, 0, 0, 0);
        // 我们使用黑色作为未映射区域的背景。
        imagefill($full_image, 0, 0, $black);

        $maximum_northing = $nothing+$radius;
        $minimum_northing = $nothing-$radius;
        $maximum_easting = $easting+$radius;
        $minimum_easting = $easting-$radius;
        $bottommost_tile_northing = floor($minimum_northing/250)*250;
        $topmost_tile_northing = ceil($maximum_northing/250)*250;
        $leftmost_tile_easting = floor($minimum_easting/250)*250;
        $rightmost_tile_easting = ceil($maximum_easting/250)*250;

        for($tile_northing=$bottommost_tile_northing;
            $tile_northing<=$topmost_tile_northing;
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
            imagecopy($full_image, $tile, $full_image_x, $full_image_y, 0, 0, 100,
                100);
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
        $retun = substr($this->png_data, 0, $bytes);
        $this->png_data = substr($this->png_data, $bytes);
        return $retun;
    }

    function stream_write()
    {
        return false; // 我们不写入数据，傻瓜。
    }

    function stream_eof()
    {
        return $this->png_data == 0;
    }

    function stream_tell()
    {
        return $this->data_length - strlen($this->png_data);
    }

    function stream_seek()
    {
        return false;
    }

    function stream_flush()
    {
        return false; // 我们不存储数据，傻瓜。
    }

    function stream_stat()
    {
        return false;
    }
}

// 我们将流包装器注册放在这里，连同它注册的
// 包装器一起，以省去每次包含文件时都要记得注册的麻烦。
//
// 这当然假设我们不会受到诱惑将相同的
// 包装器协议 (nzmg) 用于不同类型的流。
stream_wrapper_register('nzmg', 'orthophoto_stream');
?>
```

如代码最后一行所述，此类以 `nzmg` 协议注册。此处实现的 `nzmg` URL 完整格式为 `nzmg://nnnnnnneeeeeeeerrrrrr`，其中七个数字分别指定北向坐标（奥克兰地区为 6460000 至 6489750 之间的特定米数）、东向坐标（2650000 至 2689750 米之间）和半径（也以米为单位，虽然要求超过 20000 米意义不大，因为那是整个 16 × 12 公里图像的对角线长度）。

之所以使用“北向”和“东向”而非经纬度来表示位置，是因为地球既不是完美的球体，甚至也不是特别对称的扁球体，从一种坐标转换到另一种绝非易事。本例中采用的新西兰地图格网是通过经验确定的，由此产生的经纬度-北向/东向映射涉及诸如评估六度复变多项式等操作。（测量局局长办公室的精确规范可作为 `OSGC` 技术报告 4.1 获取，并可在 `LINZ` 网站上获得。）这与本例的目标无关，正如将地标和递送地址映射到坐标的练习一样无关。同样，输入数据验证的问题，包括将半径限制在比 20 公里更合理的范围内，也与此阶段无关。所有此类具体任务都应在到达此阶段之前处理完毕，使其尽可能具有广泛的适用性。
