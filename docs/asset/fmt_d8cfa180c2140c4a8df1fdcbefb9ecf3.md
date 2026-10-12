
使用 `data.Get()`，`Listing 5` 在第 34 行从一堆 `Exif` 标签数据中检索 `Orientation` 标签的值。如果未找到该标签，则无需执行任何操作，因为图像已经具有正确的方向。但是，如果程序找到了标签，第 40 行获取该标签的第一个整数值（索引 `0`），并从第 45 行开始的 `switch` 结构确定图像需要哪种纠正旋转（90 或 180 度）并调用修改函数。

**`Listing 3: imgmod.go`**

```go
01  package main
02
03  import (
04      "image"
05      "image/jpeg"
06      "log"
07      "os"
08  )
09
10  func imgMod(srcFile string, dstFile string, cb func(image.Image) *image.RGBA) {
11      f, err := os.Open(srcFile)
12      if err != nil {
13          log.Fatalf("os.Open failed: %v", err)
14      }
15
16      jimg, _, err := image.Decode(f)
17      if err != nil {
18          log.Fatalf("image.Decode failed: %v", err)
19      }
20
21      dimg := cb(jimg)
22      if err != nil {
23          log.Fatalf("Modifier failed")
24      }
25
26      f, err = os.Create(dstFile)
27      if err != nil {
28          log.Fatalf("os.Create failed: %v", err)
29      }
30
31      err = jpeg.Encode(f, dimg, nil)
32      if err != nil {
33          log.Fatalf("jpeg.Encode failed: %v", err)
34      }
35  }
```

![](img/8286bf901ba268fe114d66ada92d1dd6_53_0.png)

图 4：`Gimp` 检测到图像需要旋转 90 度。

![](img/8286bf901ba268fe114d66ada92d1dd6_54_0.png)

**图 5：** 图像顺时针旋转 90 度后的矩阵变换。

**`Listing 4: rotate-90.go`**

```go
01 package main
02
03 import (
04 	"image"
05 )
06
07 func rot90(jimg image.Image) *image.RGBA {
08 	var bounds = jimg.Bounds()
09 	width, height := bounds.Max.X, bounds.Max.Y
10 	var dim = image.NewRGBA(&image.Rect{
	Max: image.Point{X: width, Y: height}
	Min: image.Point{}})
11
12 	dim := image.NewRGBA(bounds)
13
14 	for y := 0; y < height; y++ {
15 		for x := 0; x < width; x++ {
16 			org := jimg.At(x, y)
17 			dim.Set(height-y, x, org)
18 		}
19 	}
20 
21 	return dim
22 }
```

## 商店

`shop.linuxnewmedia.com`

- 在 `Linux New Media` 的在线商店探索过去并投资新一年的 `IT` 解决方案。

- 想要订阅？正在寻找你真的很想在报摊上买的那本过刊？

➤ `shop.linuxnewmedia.com`

## 数字与印刷订阅

![](img/8286bf901ba268fe114d66ada92d1dd6_54_1.png)

## 特别版

![](img/8286bf901ba268fe114d66ada92d1dd6_54_2.png)

### 深入解析

#### 编程快照 – 使用 `Go` 旋转照片

##### 清单 5: `autorot.go`

```go
package main

import (
    "flag"
    "fmt"
    "github.com/twcarns1n/goexif/exif"
    "os"
    "path"
)

func main() {
    flag.Usage = func() {
        fmt.Printf("Usage: %s jpg-file\n", path.Base(os.Args[0]))
        os.Exit(1)
    }

    flag.Parse()
    if len(flag.Args()) != 1 {
        flag.Usage()
    }

    jpgFile := flag.Arg(0)

    f, err := os.Open(jpgFile)
    if err != nil {
        panic(err)
    }

    data, err := exif.Decode(f)
    if err != nil {
        panic(err)
    }

    orient, err := data.Get(exif.Orientation)
    if err != nil {
        fmt.Printf("No orientation header found.\n")
        os.Exit(0)
    }

    val, err := orient.Int(0)
    if err != nil {
        panic(err)
    }

    switch val {
    case 3:
        imgMod(jpgFile, jpgFile, rot180)
    case 6:
        imgMod(jpgFile, jpgFile, rot90)
    default:
        panic("Unknown orientation")
    }
}
```

使用 `imgMod` 并传入适当的算法函数作为参数。`Listing 5` 中对 `imgMod()` 的调用对源文件和目标文件使用了相同的名称，因此 `autorot` 只是简单地覆盖原始文件。如果这显得太过危险，您可以将目标文件重命名为 `.bak`，这样可以确保不会发生事故。

当 `Go` 的图像库将 `JPEG` 图像写回磁盘时，它完全省略了原始的 `Exif` 数据，因此头部中不再存在指示正确旋转的 `orient` 条目。

##### 编译程序

您可以使用 `Listing 6` 中的命令序列来创建 `autorot` 二进制文件。`go` 编译器从 `GitHub` 获取所需的库，编译它们，并将它们链接在一起。与往常一样，这会生成一个已经包含所有依赖项的可执行文件。它可以毫无问题地复制到另一台计算机上，并在该计算机上运行而不发出任何抱怨，前提是操作系统和处理器架构相似。

##### 清单 6: 编译 `autorot`

```bash
$ go mod init autorot
$ go mod tidy
$ go build autorot.go rotate-90.go rotate-180.go imgmod.go
```

![](img/8286bf901ba268fe114d66ada92d1dd6_55_0.png)

### 结论

该程序远非完美。它对大多数情况都能起作用，但仍然缺少逆时针旋转以及针对更奇特 `Exif` 值的算法。但凭借所描述的基础知识，可以轻松添加这些功能。与往常一样，`Go` 并未对爱好者设限。

**信息**

1. 本文的清单：[http://ftp.linux-magazine.com/pub/listings/linux-magazine.com/257](http://ftp.linux-magazine.com/pub/listings/linux-magazine.com/257)

2. `Mike Schilli` 的文章“在手机照片中操纵存储的地理坐标”，载于《`Linux` 杂志》240 期，2020 年 12 月，[https://linux-magazine.com/issues/2020/240/Obfuscation-Filter](https://linux-magazine.com/issues/2020/240/Obfuscation-Filter)
