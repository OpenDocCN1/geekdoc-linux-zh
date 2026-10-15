
该脚本处理包含空格的文件名时可能会出现问题。当然，打算放在网络服务器的文件名永远不应该包含空格，但你仍然应该修复脚本来消除这个问题。

## #97 创建图像缩略图

我们惊讶于这个问题出现得如此频繁：有人要么在网页上包含一张大得图像，要么通过电子邮件发送一张比电脑屏幕大得多的照片。这不仅令人恼恼，而且浪费带宽和计算机资源。

此脚本将根据你提供的任何图片创建缩略图，允许你指定详细的高度和宽度参数，或者指示生成的较小图像必须适应某些尺寸范围。事实上，创建缩略图是酷酷 `mogify` 工具的官方推荐用法：

```bash
$ mkdir thumbs
$ mogify -format gif -path thumbs -thumbnail 100x100 *.jpg
```

注意，通常你希望在并行目录中创建缩略图，而不是与原始图像相同的目录中。事实上，如果使用不当，`mogify` 工具可能是危险的，因为它可以用缩略版本覆盖目录中的所有图像，从而破坏原始副本。为了缓解这种担忧，`mogify` 命令会在 `thumbs` 子目录中创建 100 × 100 的缩略图，并在过程中将它们从 JPEG 转换为 GIF。

这很有用，但应用范围仍然窄。让我们创建一个更通用的缩略图处理脚本，如列表 14-7 所示。它完全可以用于完成上述任务，也可以用于许多其他图像缩减任务。

## 代码

```bash
#!/bin/bash
# thumbnails--为指定的图形文件创建缩略图，
# 匹配精确尺寸或不超出尺寸

convargs="-Ounsharp 0.5x -resize"
count=0; exact=""; fit=""

usage() {
  echo "Usage: $0 (-e|f) thumbnail-size image [image] [image]" >&2
  echo "-e 到精确尺寸，忽略原始比例" >&2
  echo "-f 将图像适应指定的尺寸，保留比例" >&2
  echo "-s strip EXIF 信息 (为网络使用做准备)" >&2
  echo " 使用 WIDTHHEIGHT 获取请求的尺寸 (例如， 100x100)"
  exit 1

############
## 开始主程序

if [ $ -eq 0 ]; then
    usage
fi

while getopts "e:f:s" opt; do
    e) exact="$OPTARG";
    f) fit="$OPTARG";
    s) strip="-$OPTARG";
    ?) usage;
esac
done
shift $(($OPTIND - 1)) # 消耗所有已解析的参数。

rwidth="$(echo $exact $cut | cut -dx "f1")
height="$(echo $exact $fit | cut -dx "f2")"

width="$(identify -format "%w" "$image")"
height="$(identify -format "%h" "$image")"

if [ $width -le $rw -a $height -le $rh ]; then

    echo "图像已小于请求尺寸。跳过。"

    # 构建新文件名。

suffix="$(echo $image | rev | cut -d. -f1 | rev)"
prefix="$(echo $image | rev | cut -d. -f2 | rev)"
newname="$prefix-thumb.$suffix"

# 根据需要添加 "!" 后缀以忽略比例。

if [ -z "$fit" ]; then
    size="$exact!"
    echo "为文件 $image 创建 ${width}x${height} (精确尺寸) 缩略图"
else
    size="$fit"
    echo "为文件 $image 创建 ${width}x${height} (最大尺寸) 缩略图"
fi

convert "$image" -strip $convargs "$size" "$newname"
count=$((count + 1))
done

if [ $count -eq 0 ]; then
  echo "警告：未找到待处理的图像。"
fi

exit 0
```

列表 14-7：缩略图脚本

## 它是如何工作的

ImageMagick 是如此复杂，它急需像这样的脚本来简化常见任务。在这些脚本中，我们利用了一些额外功能，包括使用 `-strip` 参数来移除可交换图像文件格式 (`EXIF`) 信息，这些信息对于照片存档有用，但对于在线使用是不必要的（例如，使用的相机、照片的 ISO 速度、f 圈、地理位置数据等）。

新的标记是 `-unsharp`，这是一个过滤器，可以确保缩小后的缩略图不会因为处理而变得模糊。解释此参数的潜在值以及它们如何影响结果将涉及大量的科学，所以为了保持简单，我们使用了这个。

想知道更多关于精确尺寸和适应尺寸的差异？查看图 14-3。

![](img/954a28cc04c09826495e330f44c0085b_352_0.png)

![](img/954a28cc04c09826495e330f44c0085b_352_1.png)

![](img/954a28cc04c09826495e330f44c0085b_352_2.png)

图 14-3：精确尺寸与适应尺寸的差异

此脚本将 `EXIF` 信息转换为后一种格式，以便你直接将数据复制并粘贴到映射程序中。在此过程中，脚本必须解决一些基础方程（注意，`identify` 工具提供的纬度第二个值为 1983/100，它等于 19.83）。

## 代码部分

纬度和经度的概念比你想象的要早。事实上，葡萄牙制图师彼得罗·雷因尔（Pedro Reinel）最早在 1504 年就在他的地图上绘制了纬度线。这些计算还涉及一些特殊的数学方法。幸运的是，我们不需要自己计算它们。相反，我们只需要知道如何将 `EXIF` 纬经度值转换为映射应用程序期望的值，即可，如列表 14-9 所示。此脚本还使用了第 33 页脚本 8 中的 `echo` 脚本。

```bash
#/bin/bash
# geoloc- 带有 GPS 信息的图像，将这些数据转换为
# 可以提供给 Google Maps 或 Bing Maps 的字符串

tempfile="tmp/geoloc.$$"
trap "$(which rm) -f "$tempfile" 0 1 15

if [ $# -eq 0 ]; then
  echo "Usage:$(basename $0) image" >&2
  exit 1
fi

for filename
do
  identify -format="%[EXIF:*]" "$filename" | grep GPS > $template

  latdeg=$(head -1 "$template" | cut -d, -f1 | cut -d, -f2)
  latdeg=$(bc -p 0 $latdeg)
  longdeg=$(head -1 "$template" | cut -d, -f2)
  longdeg=$(bc -p 0 $longdeg)
  latsec=$(head -1 "$template" | cut -d, -f3)
  latsec=$(bc -p 0 $latsec)
  latorientation=$(sed -n '2p' "$template" | cut -d, -f2)

  longdeg=$(sed -n '3p' "$template" | cut -d, -f1 | cut -d, -f2)
  longdeg=$(bc -p 0 $longdeg)
  longmin=$(sed -n '3p' "$template" | cut -d, -f2)
  longmin=$(bc -p 0 $longmin)
  longsec=$(sed -n '3p' "$template" | cut -d, -f3)
  longsec=$(bc -p 0 $longsec)
  longorientation=$(sed -n '4p' "$template" | cut -d, -f2)

  echo "Codes: ${latdeg} ${latsec} ${latorientation},"
  echo "longdeg ${longdeg} ${longsec} ${longorientation}"
done

exit 0
```

列表 14-9：geoloc 脚本

## 工作原理
