
`sudo journalctl --since yesterday`

# 显示从昨天以来所有的日志

```bash
[root@localhost manju]# ipcs -u

------ Messages Status -------
allocated queues = 0
used headers = 0
used space = 0 bytes

------ Shared Memory Status -------
segments allocated 4
pages allocated 2432
pages resident 319
pages swapped 0
Swap performance: 0 attempts 0 successes

------ Semaphore Status -------
used arrays = 0
allocated semaphores = 0
```

显示进程间通信（IPC）设施的使用状态

```bash
dmidecode -t 16
```
# 显示系统支持的最大 RAM

```bash
dmidecode -t baseboard
```
# 显示所有与系统主板的信息

```bash
dmidecode -t bios
```
# 显示 BIOS 信息

# 命令:

```bash
dmidecode -t system
```

# 描述:

显示关于系统的制造商、型号和序列号

![](img/69fdaac95fca1cdd9f4079cb7470b3aa_268_0.png)

> Linux 哲学是“面对危险大笑”。哦，错了。“自力更生”。是的，就是这个。

林斯·托瓦尔斯（Linus Torvalds）

```bash
nmcli con show -a
```
# 显示激活的网络连接

```bash
netstat -r
```
# 显示内核路由表

```bash
yum install nmap
```
# 在 CentOS 上安装 nmap

```bash
nmap google.com
```
# 扫描主机名

```bash
nmap 193.169.1.1
```
# 扫描 IP 地址

```bash
nmap --iflist
```
# 显示主机接口和路由

```bash
echo [![:digit:]]*
```
# 打印所有不以数字开头的文件和文件夹

```bash
echo *[[:lower:]123]
```
# 打印所有以小写字母或数字结尾的文件和文件夹

```bash
echo g*
```
# 打印所有以 "g" 开头的文件和文件夹

```bash
echo b*.txt
```
# 打印所有以 "b" 开接任意字符并以 ".txt" 结尾的文件和文件夹

```bash
echo [abc]*
```
# 打印所有以 "a","b" 或 "c" 开头的文件和文件夹

```bash
netstat -t
```
# 显示活动连接的下载状态

```bash
netstat -x
```
# 显示网络 Direct 的所有连接、监听器和共享端点的信息

```bash
netstat -n
```
# 地址和端口号的数字化显示

```bash
echo $LANG
```
# 显示 Linux 系统的语言

```bash
echo "AAA" | grep AAA
→ AAA
echo "BBB" | grep -E 'AAA|BBB'
→ BBB
```

```bash
echo "AAA" | grep BBB
→ 
```

```bash
echo "AAA" | grep -E 'AAA|BBB'
→ AAA
```

```bash
echo "albert einstein" | tr a-z A-Z
-> ALBERT EINSTEIN
```

```bash
echo "albert einstein" | tr [:lower:]] E
-> EEEEEE EEEEEEE
```

```bash
echo "Albert Einstein was a German-born theoretical physicist." | fold -w 12
```

![](img/69fdaac95fca1cdd9f4079cb7470b3aa_271_0.png)

```bash
echo " Albert Einstein was a German-born theoretical physicist." | fold -w 12 -s
```

![](img/69fdaac95fca1cdd9f4079cb7470b3aa_271_1.png)

```bash
printf "English theoretical physicist: %s\n" Hawking
-> English theoretical physicist: Hawking
```

```bash
ls /usr/bin | pr -3 -w 65 | head
```
# 以分页、三列输出格式显示 `/usr/bin` 的目录列表

```bash
for i in A B C D; do echo $i; done
```

```bash
Scientists=("Einstein" "Hawking" "Darwin"); for i in ${Scientists[@]}; do echo $i;
```

![](img/69fdaac95fca1cdd9f4079cb7470b3aa_272_0.png)

![](img/69fdaac95fca1cdd9f4079cb7470b3aa_272_1.png)

```bash
for i in {A..D}; do echo $i; done
```
