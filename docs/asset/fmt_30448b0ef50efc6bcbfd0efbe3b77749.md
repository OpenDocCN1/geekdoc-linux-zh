
![](img/74418f52d5d454acca60721059dbdc99_396_0.png)

## subtree selection dialog

可以使用以下命令：

```
pwd

ls <path>

cd <path>

add <path>

delete <path>

extract

quit

help
```

对于 IRIX `xfsrestore`，我必须提供比传统恢复多几个标志。`-J` 表示不更新记录，因为这是一个测试示例。`-a` 指定 `xfsrestore` 存储其将创建的临时目录的位置，它将创建该目录以执行恢复，而 `. /` 指定了恢复的目标目录。

然后我执行了 `ls`：

```
-> ls
29891968 .desktop/
52998 .profile
16810848 .cosmcreate/
285 floppy/
52995 .login
833368 lib64/
2097164 lib32/
164164 sgresources
17560127 desktop-RYOKO/
5579597 hosts/
52999 .varupdate
52996 .wshttymode
164163 public/
21057518 desktop-WAASHU/
52995 debug
16810849 patches/
8388737 stand/
74179 cabsr
2967285 nmail/
25554696 Desktop/
2967389 share/
16793345 CDROM/
63767 PlayG.map
52993 public_html
164162 .backgrounds
132 .webcache/
20971650 .netscape/
29777 unix
1688063 dumpster/
29360258 sbin/
4194435 proc/
29891969 .web/
8388739 var/
4194468 usr/
63743 tmp/
29360441 opt/
16806975 net/
12583274 lib/
16793508 etc/
16798532 dev/
3624 bin
12972039 ns/
136 hw/
```

在传统恢复中，以 `/` 结尾的文件表示目录。注意所有内容并没有按照任何逻辑顺序排列。这里的数字并不表示文件大小。

接下来，我 `cd` 到我想去的地方并提取我想要的：

```
-> cd patches
-> ls
  16810856 patchSG0003262
  16810855 README.patch.326
  16810857 patchSG0003262.oe__sw
  16810858 patchSG0003262.idb
  16810854 patchSG0003262.tar
```

```
-> add patchSG0003262.tar
-> extract
```

```
end dialog
fsrestore: examining media file 1
fsrestore: examining media file 2
fsrestore: examining media file 3
fsrestore: examining media file 4
fsrestore: seeking past media file directory dump
fsrestore: restoring non-directory files
fsrestore: read_record encountered EOD: end of data
fsrestore: 1/0 metrics: 3 by 240KB ring; 1128/1148 (98%) records
streamed;
fsrestore: restore complete: 004 seconds elapsed
464122B/s
```

`fsrestore` 将文件恢复到原始层次结构中的当前目录。例如 `patches/patchSG0003262.tar`。

```
WAASHU restore_test 4 #ls -1 patches
total 3440
-rw-r--r-- 1 root      sys       1761280 Oct 8 05:23 patchSG0003262.tar
```

## 第 13 天

以下是原始 `/patches` 目录的样子：

```
WAASHU restore_test 6 #>ls -l /patches
total 6872
-rw-r--r-- 1 root sys 3703 Jul 20 16:12 patchSG0003262
-rw-r--r-- 1 root sys 644 Jul 20 16:00 patchSG0003262.eoe_sw
-rw-r--r-- 1 root sys 174150 Jul 20 16:00 patchSG0003262.soe
-rw-r--r-- 1 root sys 1673 Jul 20 16:00 patchSG0003262.idb
-rw-r--r-- 1 root sys 176280 Oct 8 05:23 patchSG0003262.tar
```
