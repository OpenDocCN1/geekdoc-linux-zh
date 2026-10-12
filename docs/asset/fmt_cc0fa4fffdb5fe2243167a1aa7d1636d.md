
## 创建软件包仓库

- 创建仓库的目录结构。例如，对于 `apt` 仓库，你需要 `pool`、`dists` 等目录。
- 将你的软件包复制到 `pool` 目录，并根据包名和版本进行放置。
- d) 在 `dists` 目录下创建 `Packages` 和 `Release` 文件。`Packages` 文件包含仓库中所有可用软件包的列表，而 `Release` 文件包含有关仓库的信息，如版本、发布日期等。
- e) 设置你的 `sources.list` 文件以添加指向你仓库的链接。对于 `apt` 仓库，该文件位于 `/etc/apt/sources.list.d/` 目录。
- f) 为包管理器运行包缓存更新。

## 练习 14

你需要为 Linux 上的 `dpkg` 创建自己的软件包仓库，这对于本地使用或分发自己的软件包非常有用。

## 练习 15

如何在 Linux 机器上安装 Python 编程软件？

## 练习 16

如何使用特殊的 `PyInstaller` 工具为 Python 应用创建安装文件？

## 练习 17

如何在运行 Linux 操作系统的计算机上启动服务（或守护进程）？

## 练习 18 无答案

为了观察不同图形界面之间的差异，作为练习的一部分，你应该在不同的图形界面下下载并安装“SpiralLinux”软件（参见图 4.1）。为此，它们需要分别安装在安装在你操作系统上的虚拟机上；请注意这些程序之间系统元素交互方式的差异。

### 需要遵循的步骤

**步骤 1：**
为操作系统安装一个虚拟化软件产品，例如从官方网站 `https://www.virtualbox.org` 下载 `VirtualBox`；

**步骤 2：**
从开发者网站下载所有版本的“SpiralLinux”操作系统发行版：`https://spirallinux.github.io/#download`。它们拥有不同的界面：`Cinnamon`、`XFCE`、`Gnome`、`Plasma`、`Mate`、`Budgie`、`LXQt` 和“Builder”（参见图 4.1）。

**步骤 3：**
以截图（screenshot）的形式描述并注释安装你下载的 Linux “SpiralLinux”操作系统的基本步骤。

**步骤 4：**
以表格形式描述已安装操作系统界面之间的主要视觉差异，使用以下参数：便利性、清晰度、系统管理中的直观性、美观性、吸引力以及界面语言。目标表格的设计示例见表 4.1。

#### 表 4.1 – `SpiralLinux` 系统中 `GUI` 界面的比较特性

| 参数 | 便捷性 | 清晰度 | 直观性 | 吸引力 | 界面语言 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 操作系统中的各种 `GUI` | | | | | |
| `SpiralLinux` `Cinnamon` | | | | | |
| `SpiralLinux` `XFCE` | | | | | |
| `SpiralLinux` `Gnome` | | | | | |
| `SpiralLinux` `Plasma` | | | | | |
| `SpiralLinux` `Mate` | | | | | |
| `SpiralLinux` `Budgie` | | | | | |
| `SpiralLinux` `LXQt` | | | | | |
| `SpiralLinux` "Builder" | | | | | |

![](img/f7d3edbe212287bdf40c9582a51bff25_554_0.png)
`SpiralLinux` `Cinnamon`

![](img/f7d3edbe212287bdf40c9582a51bff25_554_1.png)
`SpiralLinux` `XFCE`

![](img/f7d3edbe212287bdf40c9582a51bff25_554_2.png)
`SpiralLinux` `Gnome`

![](img/f7d3edbe212287bdf40c9582a51bff25_554_3.png)
`SpiralLinux` `Plasma`

![](img/f7d3edbe212287bdf40c9582a51bff25_554_4.png)
`SpiralLinux` `Mate`

![](img/f7d3edbe212287bdf40c9582a51bff25_554_5.png)
`SpiralLinux` `Budgie`

![](img/f7d3edbe212287bdf40c9582a51bff25_554_6.png)
`SpiralLinux` `LXQt`

![](img/f7d3edbe212287bdf40c9582a51bff25_554_7.png)
`SpiralLinux` "Builder"

图 4.1 “SpiralLinux”操作系统的各种图形界面图标

# 第四章 实践练习、问题与解答

## IV.2 Linux 实践练习的解答

### IV.2.1 文件和目录管理主题练习解答

**练习 1 的解答：**
```bash
mkdir ~/mayadir
```

**练习 2 的解答：**
```bash
touch ~/mayadir/moyfile.txt
```

**练习 3 的解答：**
```bash
touch ~/mayadir/moyfile.txt
```

**练习 4 的解答：**
```bash
rm ~/mayadir
```

**练习 5 的解答：**
```bash
echo "Hello" > ~/mayadir/moyfile.txt
```

**练习 6 的解答：**
```bash
mkdir ~/mayadir
```

### IV.2.2 用户主题练习解答

**练习 1 的解答：**
```bash
sudo useradd -m alice
```

**练习 2 的解答：**
```bash
sudo passwd alice
```

**练习 3 的解答：**
```bash
sudo usermod -aG sudo alice
```

**练习 4 的解答：**
```bash
sudo userdel -r alice
```

**练习 5 的解答：**
```bash
sudo chmod 777 /var/www/html/proverka.txt
```

**练习 6 的解答：**
```bash
cat /var/www/html/proverka.txt
```

### IV.2.3 文本处理主题练习解答

**练习 1 的解答：**
```bash
echo "This is my first line in the file" > ~/moytext1.txt
echo "Here is the second line in the file" >> ~/moytext1.txt
echo "Third - the last line in the file" >> ~/moytext1.txt
```

**练习 2 的解答：**
```bash
cat ~/moytext1.txt
```

**练习 3 的解答：**
```bash
wc ~/moytext1.txt
```

**练习 4 的解答：**
```bash
#!/bin/bash
POISK_TEXT="A definite phrase"
VVOD_FILE="path/to/input/file.txt"

while read line; do
if [ "$line" == "*$POISK_TEXT*" ]; then
echo "$line"
fi
done < "$VVOD_FILE"
```

## EN IV.2.4 关于用户环境主题的练习解答

**练习 1 的解答**
```bash
date
```

**练习 2 的解答**
```bash
uname -a
```

**练习 3 的解答**
```bash
uptime
```

**练习 4 的解答**
```bash
sleep 8
```

## EN IV.2.5 关于包管理器主题的练习解答

**练习 1 的解答**
```bash
sudo apt-get install apache2
```

**练习 2 的解答**
```bash
sudo apt-get update
```

**练习 3 的解答**
```bash
sudo apt-get remove apache2
```

### 练习 4 的解答
```bash
dpkg -l vim
```

### 练习 5 的解答
要解决这个问题，我们可以使用 `grep` 命令：
```bash
grep "интерфейс" example.txt
```

### 练习 6 的解答
要做到这一点，我们可以使用 `crontab -e` 命令编辑 crontab 任务文件，并添加以下行：
```bash
0 16 * * * /path/to/script.sh
```
此行意味着 `script.sh` 将在每天 16:00 运行。让我们仔细查看参数的值：
