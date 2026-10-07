
目标是制作一个符合你个人口味的美观主题。为了实现这一点，我将从覆盖 `_common.scss` 文件中的通用定义开始。首先，为 `headerbar.titlebar` 元素定义最小值，包括窗口按钮以及定义每个包含元素外观的全局颜色定义。这正是 Canonical 为其 Ubuntu 的 Yaru 主题所做的。

然而，如果你只有一个或极少数异常情况，那么仅在文件中修改需要的部分是有意义的。`gtk.css` 中的定义列表非常庞大，超过了 2,000 行代码，你就会明白为什么大多数主题开发者只是分叉 Adwaita 主题并维护一系列覆盖，而不是从零开始掌握它们。

# 深度解析

## 自定义 GTK3 主题

浅色和深色主题的外观以及许多供应商采用了相同的方法。接下来是笔记本头部（notebook header），它代表标题栏正下方标签页区域（列表 3）。

### 修改主题

像素单位的值是我个人的估值，但它们都比 Adwaita 默认建议的要小。这里是提交更改或其他调整以修改原始样式表的恰当位置。许多 Linux 用户不喜欢 Adwaita 中宽宽的内边距和偏移。这不仅仅是审美问题——这些过于宽敞的元素占据了应用程序大量的屏幕空间，而且这些设置是随机的。你仍然需要对额外的 UI 元素定义一个小的覆盖，以便为有用内容留出更多空间。

你可能会在当前文件中发现额外的 `.scss` 文件，用于覆盖某些设计中的样式元素（列表 4）。内边距部分非常明显，但对于多个 `min-height` 值，你需要它们来确保同一区域内的元素具有一致的高度，并完美地适配到 24px 高的输入面板中。像按钮（`button`）、数字调节按钮（`spinbutton`）和 `row.activatable` 等元素的高度为 20px，并有 4px 的垂直内边距，加起来正好 24px。

#### 列表 1：gtk-light.scss

```scss
@import 'common';
```

```scss
.nautilus-window {
  .path-bar-box {
    border: 1px solid rgb(182,182,179);
    border-radius: 3px;
    &:not(:backdrop) {
      background-color: rgb(232,232,231);
    }
  }
}
```

图 2：一个好的主题不仅仅是 CSS 代码。按钮、复选框以及许多其他元素使用了外部艺术资源。

#### 列表 2：headerbar.title 元素

一旦你将文件夹移动到 `~/.themes` 并应用代码，你就需要使用桌面环境的相应工具（例如 Gnome Tweak Tool）编译 `.scss` 主题。还有一个非常实用的按钮源文件应该按如下方式处理：SASC 生成器 `gtk-widgets-factory` 命令可以让你一次性地看到所有的 GTK3 组件，并检查它们在你的主题下看起来是否正确（图 3）。

```scss
.headerbar.titlebar {
  min-height: 0;
  min-height: 16px;
  min-width: 16px;
  padding: 4px;
  &.text-button {
    min-width: 100px;
  }
}
```

```bash
$ sassc -M -t compact gtk-light.scss.css
$ sassc -M -t compact gtk-dark.scss.css
```

### 修改颜色

内边距和宽度并不总是问题所在。有时你只需要将默认样式表的颜色改为更护眼的颜色即可。如果是这种情况，请考虑将以下序列作为基础模板。

首先，复制你想要编辑的主题。找到 `_colors.scss` 文件并对其进行编辑。在大多数情况下，以下七个值用于定义调色板：`$base_color`, `$text_color`, `$bg_color`, `$fg_color`, `$selected_bg_color`, `$selected_fg_color` 和 `$top_highlight`（几乎不言自明）。通常的做法是使用 HEX 颜色值（`#343536`）或纯文本格式（`red`, `green`）。

使用 `SASSC` 转换主 `.scss` 文件。这将考虑到颜色更改：包含来自 `_common.scss` 文件的私有行，并生成最终可直接使用的 CSS 文件。剩下的工作就是重命名文件并将它们放置在正确的位置。

创建一个以主题名称命名的文件夹，然后添加 `gtk-3.0` 子文件夹，最后将你的 CSS 文件复制到子文件夹并重命名为 `gtk.css`。将主题拷贝到主题文件夹，你就可以使用新颜色的主题了。

#### 列表 3：notebook header

```scss
notebook header {
  spinbutton, button {
    margin: 0;
    min-height: 20px;
    padding: 0;
    min-width: 16px;
  }
  tabs {
    padding: 2px 4px;
    margin: 0;
  }
  tab {
    padding: 0px;
    min-height: 20px;
  }
  spinbutton {
    min-width: 42px;
    padding: 0;
    padding: 4px 12px;
    margin: 0;
  }
}
```

#### 列表 4：UI Elements

```scss
.path-bar {
  button {
    min-width: 0;
  }
}
.path-bar-box {
  padding: 1px 0;
}
entry {
  min-height: 24px;
  padding-top: 3px;
  padding-bottom: 4px;
}
switch slider {
  &.bottom tabs tab {
    min-height: 24px;
    padding-top: 4px;
    padding-bottom: 3px;
    min-width: 42px;
  }
  &.left tabs tab {
    padding-right: 16px;
  }
  row.activatable {
    min-height: 20px;
  }
  &right tabs tab {
    padding: 4px;
  }
}
```

### 使用 Oomox 进阶

`Oomox`，也称为 Themix Designer [4]，是一个用于生成自定义 GTK3 主题的图形化应用程序。`Oomox` 非常易用，它让没有经验的 Linux 用户可以在几分钟内创建自己的精美主题。该应用程序自带一系列预设，在颜色方案、UI 元素形状、内边距和尺寸上有所不同。在 `Oomox` 中选择一个预设并立即生成主题相关的设置以及最终的 CSS 文件，并将它们放在正确的文件夹中，`Oomox` 为用户节省了手动操作的精力。而且没有任何阻止你稍后检查生成的 CSS 代码。

# 编程快照 – 使用 Go 制作启动 USB 盘

创建一个带有终端界面显示的可启动 USB 盘，准备就绪，待发

一个 Go 程序将下载的 ISO 文件写入可启动的 USB 盘。为了防止其意外覆盖硬盘，Mike Schilli 为其提供了一个用户界面和安全检查。*Mike Schilli 著*

在真实硬件上测试新的 Linux 发行版时，带有 ISO 格式下载镜像的可启动 USB 盘将有助于引导安装过程。用 Go 编写一个类似的启动工具会有多难呢——一个能够主动等待 USB 盘插入，然后请求用户许可进行复制的工具，这通常带出一个让你尽情尝试的 Live 系统，可能在重启后依然可用？始终，通过自己编写工具并对 BIOS 中的启动顺序进行一些更改，你将学到一些以后解决日常新任务时可能会帮助的新技巧。

ISO 文件是如何在不同函数之间传输到优盘的？根结底，这是通过非常简单的 `dd` 命令实现的，该命令将 ISO 文件作为输入（`in`），并将 USB 盘的设备节点（例如 `/dev/sdd`）作为输出（`out`）。

## 复制的艺术

将几个 GB 大小的 ISO 文件复制到优 盘等另一个文件系统并非易事。像 Ubuntu 的“启动盘创建器”（Startup Disk Creator）之类的工具通过图形界面让事情变得更加方便，但存在一些问题。在任何情况下，`cp` 和 `dd` 都不会一次性从磁盘读取源文件的所有数据——这会占用大量宝贵的内存，而不会缩短进程。相反，此类复制工具从源文件中读取数据（通常以 MB 为单位的分块），并保持将其写入同时打开的目标文件中。

优点是保持了灵活性；你不需要因为数据源的改变而更改代码，因为接口保持不变。这正是列表 1 中的代码所做的。`cpChunks()` 函数在复制完每个数据块后向通道发送一个百分比值，表示已复制字节数占总数的比例。

为了让 Go 程序员能够汇聚许多库，接受标准的 `Reader` 和 `Writer` 接口。库函数期望调用者传递一个 `Reader` 对象的指针，然后使用 `Read()` 逐块地从中提取数据。`Reader/Writer` 接口在数据上构建了抽象，无论其来源是 Web 服务器的 JSON 流，还是通过文件描述符读取的本地文件系统块。

## 作者

Mike Schilli 在加州旧金山湾地区担任软件工程师。在他自 1997 年以来运行的专栏中，他每月研究 Go 设计：各种编程语言的实际应用。如果你通过 `mschilli@perlmeister.com` 邮件他，他乐意回答任何问题。

## Go 设计：Reader/Writer

#### 列表 1: cpchunks.go

```go
01 package main
02 import
03 (
04  "bufio"
05  "io"
06  "os"
07 )
08
09 func cpChunks(src, dst string, percent chan<- int) error {
10  total := 0
11  data := make([]byte, 4*1024*1024)
12
13  in, err := os.Open(src)
14  if err != nil {
15    return err
16  }
17  defer in.Close()
18  reader := bufio.NewReader(in)
19
20  out, err := os.OpenFile(dst, os.O_WRONLY, 0644)
21  if err != nil {
22    return err
23  }
24  defer out.Close()
25  writer := bufio.NewWriter(out)
26
27  defer out.Close()
28
29  for {
30    count, err := reader.Read(data)
31    total += count
32    data = data[:count]
33
34    if err == io.EOF {
35      break
36    } else if err != nil {
37      return err
38    }
39
40    _, err = writer.Write(data)
41    if err != nil {
42      return err
43    }
44  }
45  fi, err := in.Stat()
46  if err != nil {
47    return err
48  }
49
50  percent <- int(int64(total) * int64(100) / fi.Size())
51  return nil
52 }
```

# 编程快照 – 使用 Go 制作启动型 USB

第 19 行中的行程中并行运行。与此同时，再次读取当前设备项，使用 `strconv` 包将字符串转换为整数，函数进行到最后并再次循环。如果发现新设备，第 58 行将结果除以 1MB，从而将容量转换为 GB。如果新创建的驱动器 `drivech` 不在 `seen` 映射表中，第 29 行将通道 `channel` 复制给调用者，以便在初始化阶段后报告新发现的驱动器。主程序在急切等待 `drivech` 通道后从那里获取它。该函数返回一个格式化良好的字符串值，以便第 56 行的用户在阻塞状态下（但在 Go 程中是异步的）在 UI 中进行重新验证，以确保它确实是 USB 盘而不是一个（大得多的）硬盘。与此同时，在后台保持活跃的 Go 程在无限循环中运行。结果如列表 3 所示。

## 驱动器发现

为了发现 USB 的的容量，列表 2 在第 43 行运行了 `sfdisk -s /dev/sdd` 命令。在 `for` 循环的第一轮通过后，标准输出检查了所有现有设备，在 Go 中通过 `os.Exec` 包包含标准输出。这对于表示 U 盘容量（单位为 KB）的单个整数值尤其如此。第 52 行删除了结果字符串中的换行符。第 53 行使用了我们看过的 `termui` 终端 UI 中的 `Atoi()`。

### 使用 UI 更好

带有用户界面的工具（即使仅是终端应用程序）也比仅使用要求用户选择或确认条目的标准的工具要易用得多。现在事情开始快速进行。`for` 循环在第 34 行的 `Sleep` 语句后反复触发，列表 3 中的主程序使用了 `termui` 终端 UI。

#### 列表 2: drive.go

```go
package main

import (
	"bytes"
	"errors"
	"fmt"
	"os/exec"
	"path/filepath"
	"strconv"
	"strings"
	"time"
)

func driveSize(path string) (string, error) {
	var out bytes.Buffer
	cmd := exec.Command("sfdisk", "-s", path)
	cmd.Stderr = &out
	err := cmd.Run()
	if err != nil {
		return "", err
	}
	sizeStr := strings.TrimSuffix(out.String(), "\n\n")
	size, err := strconv.Atoi(sizeStr)
	if err != nil {
		return "", err
	}
	return fmt.Sprintf("%.1f GB", float64(size)/float64(1024*1024)), nil
}

func driveWatch(done chan error) chan string {
	drivech := make(chan string)
	seen := map[string]bool{}
	init := true
	go func() {
		for {
			dpaths, err := devices()
			if err != nil {
				done <- err
				return
			}
			for _, dpath := range dpaths {
				if _, ok := seen[dpath]; !ok {
					seen[dpath] = true
					if !init {
						drivech <- dpath
					}
				}
			}
			time.Sleep(1 * time.Second)
		}
	}()
	return drivech
}

func devices() ([]string, error) {
	devices := []string{}
	paths, _ := filepath.Glob("/dev/sd*")
	if len(paths) == 0 {
		return devices, errors.New("No devices found")
	}
	for _, path := range paths {
		devices = append(devices, path)
	}
	init = false
	return devices, nil
}
```

#### 列表 3: isoflash.go
