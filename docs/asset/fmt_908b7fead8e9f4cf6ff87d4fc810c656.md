
```
mergerfs -c default,other,allow /media/a/b:/media/a/c:/media/a/d:/media/a/e /media/a/merged
```

LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM | 第254期 2022年1月 39

# 深度编程快照 – Go 和 Fyne

## 使用 Go 和 Fyne 丢弃照片失败

## 麦穗与谷壳

如果你只想从数字收藏中保留好的照片，就必须找到并删除那些失败的作品。Mike Shilli 使用 Go 和 Fyne 框架编写了一个实用程序，帮助你整理照片库。作者：Mike Shilli

![](img/28ca43fc7e7266abd9ae8dd9cb34448b_39_0.png)

![](img/28ca43fc7e7266abd9ae8dd9cb34448b_39_1.png)

列表 1：`img.go`

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/canvas"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
	"os"
)

func main() {
	wapp := app.New()
	win := app.NewWindow("img")
	img := canvas.NewImageFromFile("test.png")
	img.Resize(fyne.NewSize(600, 400))

	button := widget.NewButton("Quit", func() {
		os.Exit(0)
	})

	content := container.NewVBox(img, 
	tbutton)
	win.SetContent(content)
	win.ShowAndRun()
}
```

Go 的命令行程序虽然很好，但你还需要一种方法来显示加载的照片、过滤它们并丢弃那些失败的。根结底，如果没有一个好的画册，你的手机将毫无用处。

关于与 Electron 连接以及主跨平台 UI 开发世界的见解。在本期中，可以很容易地用 Go 写一个照片杀手器。

Reilly 最近出版的《Linux Magazine》介绍了一些使用 Fyne 的示例 [2]，但真正的应用程序还需要一些额外的润色。列表 [3] 显示了我第一次尝试创建一个照片应用，它以新方式显示 JPEG 并带有一个退出功能。照片可以追溯到我 2021 年最近一次的德国之旅，当时我开始追踪从柏林到 Bad Titz 之间德国伟大的宠物烘焙师。在这里，该程序更适合从命令行调用，并带有来自德国东南边缘 Lengriegs 的绝妙前言。我与照片和退出按钮之间持续的斗争在于，从磁盘加载一张 4032x304 分辨率的照片并显示在应用程序窗口中需要两秒钟。

## 构建一个用于图像排序的工具

# 作者

Mike Shilli 在加利福尼亚州旧金山湾担任软件工程师。特别是，他已经运行了1999 年。如果你需要帮助，可以通过 `shilli@permail.com` 联系他。

# 深度编程快照 – Go Fyne

### 列表 2：inuke main

```go
001 package main
002
003 import (
004 	"container/list"
005 	"os"
006 	"fyne.io/v2"
007
008 	"fyne.io/v2/app"
009 	"fyne.io/v2/storage"
010 	"fyne.io/v2/container"
011 	"fyne.io/v2/canvas"
012 	"fyne.io/v2/widget"
013
014 	"github.com/hashicorp/golang-lru"
015
016 var Cache *inuke.Cache
017
018 func main() {
019 	win := app.New().NewWindow("Inuke")
020
021 	var err error
022
023 	Cache, err := lru.New(128)
024 	panicOnErr(err)
025
026 	cwd, err := os.Getwd()
027 	panicOnErr(err)
028
029 	dir, err := storage.ListForUI(cwd)
030 	storage.NewWithFileUI(cwd)
031 	panicOnErr(err)
032
033 	files, err := dir.List()
034 	panicOnErr(err)
035
036 	images := list.New()
037
038 	for _, file := range files {
039 	if os.IsDir(file) {
040 	images.PushBack(file)
041 	}
042 	}
044
045 	if images.Len() == 0 {
045 	panic("No images found")
046 	}
047
048 	cur := images.Front()
049
050 	img := canvas.NewImageFromResource(nil)
051 	img.SetSize(win.Size())
052 	fyne.Resize(win.Width, win.Height)
053
054 	bl := widget.NewNewLabel(nil)
055 	"[H] Left [Right] [Delete] [Quote]"
```

```go
090 func scrollLeft(l *list.List,
091 	el *list.Element) *list.Element {
092 	if el == nil {
093 		return nil
```

# 深度编程快照 - Go Fyne

从第 62 行开始的回调例程。对于一个等待鼠标点击的 GUI 来说，拦截按键是相当奇特的。但 Fyne 允许这样做，而且有了键盘，我就可以像恶鬼魂入你的房子一样移动鼠标。按下 `L` 向右移动，`H` 向左移动，`D` 删除当前帧并使用 `refresh()` 接收循环，即“旧”目录。

![](img/28ca43fc7e7266abd9ae8dd9cb34448b_42_0.png)

主程序中的事件循环，它首先将 GUI 显示在屏幕上，并通过 `win.Run()` 极快地响应输入。

图 3：在一个双向链列表中，用户尽管存在间隙也可以来滚动。

## 带有房屋的数组

将文件 URL 作为在 Fyne 框架结构选择中的路径。Fyne 用于抽象路径的机制是因为并不是所有的操作系统都提供对文件系统的访问。例如，手机可以从……获取数据。

得益于 Fyne 的抽象层，后续函数处理数据完全透明。

按键被函数拦截，提供了一个……

那么，主程序是如何提议通过一种 derish 高效管理用户对象列表的，在这里交付一个这里和那个

### 列表：image.go
