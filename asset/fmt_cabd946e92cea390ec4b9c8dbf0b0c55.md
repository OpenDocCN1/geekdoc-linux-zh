
# 教程 — IMAGEMAGICK LINUX 语音

如果你想像列表 6 所示重建图 1 中的示例定居点，表 1 解释了组装工具和复合工具的含义，以及创建新图像过程中的其他内容。这使得查看 `ImageMagick` 变得更有意义。

## 结论

`ImageMagick` 与 DIY shell 脚本结合时会变成一个非常强大的工具。当然，你仍然可以处理现有的图像。然而，如果有必要，你可以自动化创建新图像的流程。

## 信息

- [1] `ImageMagick`: `https://imagemagick.org/index.php`
- [2] 内置测试、填充模式等：`https://imagemagick.org/script/formats.php`
- [3] X-Window 名称：`https://imagemagick.org/script/color.php`
- [4] 等离子体渐变：`https://legacy.imagemagick.org/Usage/canvas/plasma`
- [5] 创建画布：`https://legacy.imagemagick.org/Usage/canvas/gradient`

## 作者

`Ralf Kirchner` 在一家软件和系统供应商担任 Visual Basic 工作。`Ralf` 是一位资深系统管理员，同时也提供兼职培训。

## 列表 6: 构建天际线

```bash
echo <draw "sandybrown-primitive':rectangle \$xstr / \$" >> $mfile

echo <draw "floor-primitive':rectangle \$xstr / \$" >> $mfile

top=$X echo \$oy \$height + \$dh

left=$x

for ((i=0; i<lines; i++)); do
  echo "links-\$x + \$fa"
  for ((j=0; j<columns; j++)); do
    VarInt=$(echo \$cols / 2)
    if [ \$j -eq \$VarInt ]; then
      links-\$x + \$m
    fi
    t-\*left,top,\' \$1 + \$fb', \$expr \$top + \$fh"
    echo <draw "floor-yellow-primitive':rectangle \$t / \$" >> $mfile
    links=\$expr \$links + \$fb + \$fa
  done
  if [ \$i -ne \$lines - 1 ]; then
    t-center-left,top,center-right,\expr \$top + \$fh"
    echo <draw "floor-yellow-primitive':rectangle \$t / \$" >> $mfile
  else
    t-center-left,top,center-right, op \$rh"
    echo <draw "floor-yellow-primitive':rectangle \$t / \$" >> $mfile
  fi
  left=$x
  top=\$top + \$rh + \$dh
done

echo outputfile= filename="$1.png"
echo outputfile=$ mfile
echo </image> >> $mfile

conj: mfile=$mfile
```
