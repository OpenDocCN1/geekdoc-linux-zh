
# 附录 E 示例脚本

本附录提供了 Notes 操作的脚本列表。

## E.1 start_domino.sh

```bash
#!/bin/bash

NOTES_USER=notes # Notes 用户
NOTES_PATH=/home/notes # 目录
NOTES_DATA=/opt/notesdata/ # Domino 目录
SERVER=/opt/lotus # Domino 位置
SERVER_NAME=${SERVER##*/} # Domino 服务器名称
OUTPUT_LOG=/var/log/$SERVER_NAME.log # 日志存放位置
PATH=/opt/lotus/bin:$HOME:$PATH
if [ "$USER" = "root" ]; then
    echo "不要使用 root 服务器"
    su notes
fi
if [ ! -x $SERVER/bin/server ]; then
    echo "找不到 server 命令"
    exit 1
fi
if [ ! -d $NOTES_DATA ]; then
    echo "无法访问 notes 目录"
    exit 1
fi
NOTES_RUNNING=$(ps -fu notes | awk '{print $2}' | grep /opt/lotus | \
grep -v grep | cut -d"-" -f1,2,3,4 | head -n1)
if ! "$NOTES_RUNNING"; then
    echo "Domino 服务器已经在运行"
    exit 1
fi
cd $NOTES_DATA
rm -f *.notes 2>&1
mems=$(ipcs -m | grep $NOTES_USER | awk '{ print $2 }')
sems=$(ipcs -s | grep $NOTES_USER | awk '{ print $2 }')
for j in $mems; do [ -n "$j" ]; then ipcrm $j; done

 j in $sems;; [ -n "$j"" then ipcjjj>.lck; done
rm -f tmp.lck

echo "正在 Linux 上运行 Domino"
```

## E.2 cleanup_domino.sh

```bash
#!/bin/bash

NOTES_USER=notes

NOTES_PATH=/local/notes

PATH=$NOTES_PATH:/opt/lotus/bin:$HOME:$PATH

count=0

NOTES_RUNNING='ps -fu $NOTES_USER | grep /opt/lotus | grep -v grep | grep -v bash'

while [[ -n $NOTES_RUNNING ]]; do

  sleep 10

  count=$((count + 1))

  echo "...等待 $count 秒"

  if [ $count -eq 12 ]; then

    echo "2 分钟后 Domino 服务器仍在运行"

    echo "现在将其杀死"

    for i in $(ps -m | grep $NOTES_USER | grep /opt/lotus|grep -v grep|grep -v awk '{print $2}'); do

      kill -9 $i

    done

    seps=$(ps -m | grep $NOTES_USER | awk '{print $2 }')

    sems=$(ipcs -s | grep $NOTES_USER | awk '{ print $2 }')

    for j in $seps; do [ -n "$j" ]; then ipcrm $j; done

    for j in $sems; do [ -n "$j" ]; then ipcrm $j; done

    rm -f tmp.lck

    exit

  fi

  NOTES_RUNNING='ps -fu $NOTES_USER | grep /opt/lotus | grep -v grep '

done

rm -f $NOTES_PATH/notes.lck

echo "Domino 停止完成"
```

# 附录 F 使用附加材料

本红书还包含 CD-ROM 材料。请参下文有关使用或下载 CD-ROM 材料的说明。

## F.1 使用 CD-ROM

随附红书的 CD-ROM 包含以下：

| 文件名或目录 | 描述 |
| --- | --- |
| `SG246007.html` | Windows 系统的自动运行主 HTML 文件 |
| `AUTORUN.*` | 各种 HTML 文件 |
| `*.html` | HTML 文件中使用的各种图像 |
| `*.avi` | 视频目录 |
| `Java/` | Java 程序源代码目录 |
| `htdocs/` | HTML 和 JSP 文件目录 |
| `script/` | 各种脚本文件目录 |
| `sample/Redbooks.nsf` | 示例红书 Lotus Domino 数据库 |

### F.1.1 使用 CD-ROM 的系统要求

为了优化使用 CD-ROM，推荐以下软件配置：

| 浏览器 | 描述 |
| --- | --- |
| | 如 `Internet Explorer` 或 `NetScape Navigator` |
| `Adobe Acrobat Reader` | 用于阅读 PDF 格式的红书 |
| Windows 视频/AVI 播放器 | 用于运行视频 |

### F.1.2 如何使用 CD-ROM

CD-ROM 应该自动打开浏览器窗口。如果需要手动打开 CD-ROM，可以通过将浏览器指向 CD-ROM 根目录下的 `SG246007.html` 文件并遵循找到的链接来访问 CD-ROM 或磁盘的内容。

## F.2 在互联网上查找附加材料

与本红书相关的 CD-ROM、磁盘或 Web 材料也可以通过 IBM Redbooks 服务器以软件副本在互联网上提供。将您的浏览器指向：

```
ftp://www.redbooks.ibm.com/redbooks/S9324607
```

或者，您可以访问 IBM Redbooks 网站：

```
http://www.redbooks.ibm.com/
```
