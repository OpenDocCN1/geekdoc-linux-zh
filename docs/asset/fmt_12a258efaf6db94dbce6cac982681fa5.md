
```
echo <draw "fill:brown 'rectangle 1 / '" >> $msfile

echo <draw "fill:white 'rectangle $str / '" >> $msfile

top=$oy - echo $height

left=$ox

for ((i=0; i<$lines; i++)); do

for ((j=0; j<$columns; j++)); do

varInt=$expr $cols / 2

if [ $j -eq $varInt ]; then

links=$links +$fa

fi

t=$left,top, $left,expr $top +$fb

echo <draw "fill:yellow 'rectangle $t / '" >> $msfile

links=$links +$fa

done

if [ $i -ne $lines - 1 ]; then

t=$center-left,top,$center-left,expr $top +$rh

echo <draw "fill:white 'rectangle $t / '" >> $msfile

t=$center-right,top,$center-right,expr $top +$rh

echo <draw "fill:white 'rectangle $t / '" >> $msfile

done

fi

left=$left

top=$top +$rh +$dh

done

echo outputfile= filename="$1.png" /"

echo outputfile >> $msfile

echo <image> >> $msfile

conjure:$msfile

962 2022年10 | LINUX-MAGAZINE.COM | LINUXPROMAGAGINE.COM
```

## 教程 – IMAGEMAGICK LINUX VOICE

如果你想如列表 6 所示重建图 1 中的示例布局。表 1 解释了`assembly`和`composite`工具的含义，以及创建新图像的过程。这使得查看`ImageMagick`更有价值。

### 信息

- [1] `ImageMagick`: https://imagemagick.org/index.php
- [2] 内置测试模式、填充模式等：https://imagemagick.org/script/formats.php
- [3] X-窗口颜色名称: https://imagemagick.org/script/color.php
- [4] 离子渐变：https://legacy-imagemagick.org/Usage/canvas/#plasma
- [5] 创建画布：https://legacy-imagemagick.org/Usage/canvas/#gradient

### 结论

当与`DIY shell`脚本结合时，这是一个非常强大的工具。当然，你仍然处理图像。然而，如果你可以自动化

### 作者

Ralf Kirchnerner在一家软件和供应商系统担任视觉程序员。Ralf是一位资深系统管理员，也提供自由培训。

## 列表 6: 构建天际线

```bash
$ ./buildHouse 1 8
$ ./buildHouse 2 10 0
$ ./buildHouse 3 8 10
$ ./buildHouse 4 1 250
$ magic composite house1.png house2.png house3.png house4.png -geometry +0 -tile x1 street.png
$ magic composite logo: street.png -gravity NorthEast-street.png
```
