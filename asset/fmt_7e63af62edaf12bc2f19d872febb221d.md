
那绝对不是表格的内容。通过对 `curl` 进行一些调整，你可能可以使用工具来分析这些元数据，但让我们专注于稍微简单一点：一个让你选择文件并自动镜像到你的 Google Drive 账户的脚本，详见列表 13-8。

## 代码

```bash
#!/bin/bash

# syncdrive--允许你指定一个或多个文件自动复制
# 到你的 Google Drive 文件夹，该文件夹与你的云账户同步

gdrive="$HOME/Google Drive"
ggsync="$gsync"
gapp="Google Drive.app"

if [ -eq 0 ]; then
  echo "Usage: $(basename $0) [要同步的文件或文件]" >&2
  exit 1
fi

# 首先，Google Drive 是否正在运行？如果没有，启动它。
if [ -z "$(ps -ef | grep "$gapp" | grep -v grep)" ]; then
  echo "启动 Google Drive 守护进程..."
  open -a "$gapp"
fi

# 现在，gsync 文件夹是否存在？
if [ ! -d "$gsync" ]; then
  mkdir "$gsync"
if [ $? -ne 0 ]; then
echo "$(basename $0): 创建 gsync 失败" >&2
exit 1
fi

for name in $@@ # 传递给脚本的参数。
do
  echo "正在将文件 $name 复制到你的 Google Drive"
  cp -a "$name" "$gdrive/gsync"
done

exit 0
```

列表 13-8：`gsyncrive`脚本

## 工作原理

与第 300 页的脚本 #89 类似，此脚本在将文件或文件复制到 Google Drive 文件夹之前会检查特定的服务守护进程是否正在运行。这是通过代码块完成的。为了编写整洁的代码，我们应该检查 `open` 用的返回码，我们将此留给读者的练习题，好吗？之后，脚本确保 Google Drive 上存在名为 `gsync` 的子目录，如果需要则创建它，并使用 `cp` 的 `-a` 选项将指定的文件或文件复制其中，以保留创建和修改时间。

## 运行脚本

只需指定一个或多个你希望与 Google Drive 账户同步的文件，脚本将完成所有幕后工作以确保该操作实现。

## 结果

这其实很酷。指定一个你想复制到 Google Drive 的文件，如列表 13-9 所示。

```bash
$ gsync sample.crab

启动 Google 守护进程...

正在将 sample.crab 复制到你的 Google Drive

$ gsync ~/Documents/what-expect-ed.doc

正在将 ~/Documents/what-expect-ed.doc 复制到 Drive
```

列表 13-9：启动 Google Drive 并使用脚本同步文件！

注意第一次运行时，它还需要启动 Google Drive 守护进程。等待几秒让文件复制到云存储系统后，它们将出现在 Google Drive 界面中，如图 13-1 所示。

![](img/954a28cc04c09826495e330f44c005b_340_0.png)

图 13-1：同步 Google Drive 的示例和文档会自动显示。

## 修改脚本

这里有一点虚假广告：当你指定要同步的文件时，脚本并不会与未来的文件保持同步；它只是复制一次文件就结束了。一个有趣的黑客方法是创建一个更强大的脚本版本，其中你指定想要备份的文件，并定期检查这些文件，并将任何新内容复制到 `gsync` 目录。

## #93 计算机说 . . .

OS X 包含一个复杂的语音合成系统，可以告诉你系统中的情况。它通常位于辅助功能选项中，但你可以利用一个可以说话的计算机做很多事情，例如读取错误消息或读取文件。

事实证明，这些功能——以及许多声音——也可以通过 OS X 中的命令行访问，使用一个名为 `say` 的内置工具。你可以用这个测试它：

我们知道你会觉得这很有玩！

使用内置程序可以做很多事情，但这也是编写一个封装脚本的绝佳机会，该脚本可以更容易确定安装了哪些声音，并获取每个声音的演示。列表 13-10 中的脚本并没有替换 `say` 命令；它只是让该命令更容易使用（这是本书贯穿始终的主题）。

## 代码

```
r ) rate="$OPTARG" ;
v ) voice="$OPTARG" ;;
esac
done
```

```
shift($($OPTIND - 1))
if [ $ -eq 0 -z "input" ]; then
  $dosay "Hey! You haven't given me any parameters to work with."
  echo "Error: no parameters specified. Specify a file or phrase."
  exit 0
fi
```

```
if [ "$1" = "demo" ]; then
  demovoices
  if [ ! -z "$input" ]; then
    $dosay rate -v "$voice" -f $input
  else
    $dosay rate -v "$voice" "$*"
  fi
  exit 0
fi
```

列表 13-10：`sayit` 脚本

## 工作原理

安装的声音甚至比摘要中列出的多（那些只是针对英语优化的声音）。要获取完整的声音列表，我们必须回到原始 `say` 命令并使用 `-v` 参数。以下是完整声音列表的桥接版本：

| say -v | | |
| :--- | :--- | :--- |
| Agnes | en_US | # 有一台会对你说话的电脑不是不好吗？ |
| Albert | en_US | # 我嗓子里有青蛙。我是说真的青蛙！ |
| Alex | en_US | # 大多数人通过我的声音识别我。 |
| Alice | it_IT | # Salve, molto Alice e sono una italiana. |
| --skip-- | | |
| Zarvok | en_US | # 那看起来像是一个和平的行星。 |
| Zuzana | cs_CZ | # Dobrý den, jmeni Suzana. Jsem český hlas

我们最喜欢的注释是 Pipe Organ（我们必须为这种阴森的声音感到高兴。）和 Zarvok（那看起来像是一个和平的行星）。

显然，可选的声音太多了。此外，有些声音真的破坏了英语发音。一种解决方案是通过 `en_`（或你喜欢的其他语言）进行过滤，以只获取英语声音。你可以使用 `en_US` 用于美国英语，但其他声音也值得一听。

我们在此块的末尾包含了复杂的 `sed` 替换序列，因为它并不是一个格式良好的列表：它有单单词名称（Fiona），也有双单词名称（Bad News），但空格也被用于创建列状数据。为了解决这个问题，每行中的第一个空格被转换为下划线，并删除所有其他空格。如果声音是单单词名称，它将看起来像这样：`Ralph_`，最后的替换将删除任何末尾的下划线。在此过程结束时，双单词名称带有一个下划线，因此在输出给用户时需要对其修复。然而，代码有一个良好的副作用，即使得使用默认空格分隔符编写 `while` 循环变得简单得多。

另一个有趣的部分是每个声音按顺序自我介绍的地方——`sayit` 演示调用——位于 `\.`。

一旦你理解了命令本身，这一切非常简单。

## 运行脚本

由于此脚本会产生音频，在书中你看不到什么内容，而且我们没有《Wicked Cool Shell Scripts》的音频书（你可以想象一下你看不见的东西？），你需要自己动手来体验结果。脚本列出所有安装声音的能力可以在列表 13-11 所示演示。

## 结果

```
$ say -d

Available voices: Agnes, Albert, Alex, Bad News, Bahh, Bells, Boing, Bruce, Bubbles, Cellos, Daniel, Deranged, Fred, Good News, Hysterical, Junior, Karen, Kathy, Moira, Pipe Organ, Princess, Ralph, Samantha, Tessa, Trinoids, Veena, Vicki, Victoria, Whisper, Zarvox

HANDY TIP: use "sayit.sh demo" 来听所有不同的声音

$ say "Yo, yo, dog! Whassup"

$ say -v "Pipe Organ" -r 60 "Yo, yo, dog! Whassup"

$ say -v "Ralph" -r 80 -f alice.txt
```

