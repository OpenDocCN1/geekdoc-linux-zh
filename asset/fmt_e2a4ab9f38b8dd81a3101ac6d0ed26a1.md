
```bash
Scientists=("Einstein" "Hawking" "Darwin"); for i in "${Scientists[@]}"; do echo $i;
```

![](img/69fdaac95fca1cdd9f4079cb7470b3aa_272_2.png)

![](img/69fdaac95fca1cdd9f4079cb7470b3aa_272_3.png)

```bash
for i in file*.txt; do echo $i; done
```

![](img/69fdaac95fca1cdd9f4079cb7470b3aa_272_4.png)

```bash
echo ${!BASH*}
# 列出所有以 BASH 开头的环境变量
```

```bash
<<< "6+6"
```
![](img/69fdaac95fca1cdd9f4079cb7470b3aa_272_5.png)

```bash
df -k
# 查看文件系统
```

```bash
ls -alh
# 列出目录中的所有文件夹
```

```bash
find /home -name file.txt
# 在 /home 中查找名为 file.txt 的文件
```

```bash
find /home -iname File.txt
# 在 /home 中不区分大小写查找 File.txt
```

```bash
find / -ctime +90
# 查找修改在 90 天以前的文件
```

```bash
find / -size 0
# 查找空文件
```

```bash
find / -size +1G
# 查找大于 1GB 的文件和文件夹
```

```bash
df -a
# 显示文件系统的完整磁盘使用情况
```

```bash
df -i
# 显示已用和空闲的 inode
```
![](69fdaac95fca1cdd9f4079cb7470b3aa_273_0.png)

```bash
du -ch *.
# 显示当前目录下每个文件的大小
```

```bash
du -a /etc/ | sort -n -r | head -n 10
# 列出 /etc/ 中占用空间最大的 10 个目录
```

```bash
ac
# 显示用户连接系统的总时长
```

```bash
ac --totals
# 显示各个用户的报告
```

```bash
cancel
# 取消作业
```

```bash
yum install finger
# 安装 finger 工具 (CentOS)
```

```bash
finger manju
# 显示用户 "manju" 的详情
```

```bash
chfn
# 允许修改用户信息
```

```bash
finger -s manju
# 显示用户 "manju" 的空闲状态和详情
```

```bash
id -nG
# 列出所属的所有组
```

```bash
groupadd mygroup
# 创建名为 "mygroup" 的新组
```

```bash
groupdel mygroup
# 删除名为 "mygroup" 的组
```

```bash
less /etc/group
# 列出所有组
```

```bash
usermod -aG mygroup manju
# 将现有用户 "manju" 加入组 "mygroup"
```

```bash
userdel manju
# 删除用户 "manju"
```

```bash
chgrp mygroup test.txt
# 将文件 test.txt 的所有组改为 "mygroup"
```

```bash
sudo depmod -a
# 生成所有内核依赖和关联文件的列表
```

```bash
dirname /usr/bin
-> /usr
```

```bash
dirname /root
-> /root
```

```bash
dmesg > kernel_messages.txt
# 将内核缓冲区中的所有消息写入文件 "kernel_messages.txt"
```

```bash
dmesg | grep -i memory
# 显示与内存使用相关的内核消息
```

```bash
grep -c '^Hello\|World$' myfiles.txt
# 统计 myfiles.txt 中以 'Hello' 开头或以 'World' 结尾的行数
```

```bash
vi myfiles.txt
# 编辑文件 myfiles.txt
```

```bash
expand myfiles.txt
# 将制表转换为空格并输出到标准输出
```

```bash
expand --tabs=10 myfiles.txt > myfiles.txt
# 将 myfiles.txt 中的制表转换为 10 个空格，并将输出写入 myfiles.txt
```

```bash
expr 2 = 5
# 返回 0 (假)
```

```bash
fc -1
# 列出命令历史
```

```bash
!l
# 执行最近执行的以 "1" 开头的命令
```

```bash
fc -e1
# 执行最近执行的以 "1" 开头的命令
```

```bash
fmt myfiles.txt
# 显示格式化后的文件 "myfiles.txt"
```

```bash
fmt < myfiles.txt > myfiles.txt
# 重新格式化 "myfiles.txt" 并输出写入文件 myfiles.txt
```

```bash
finger -p manju
# 显示关于用户 "manju" 的信息
```

```bash
fold -w5 myfiles.txt > myfiles.txt
# 将 myfiles.txt 的行折宽限制为 5 个字符，并将输出写入 myfiles.txt
```

```bash
for file in *.txt ; do -l $file ; done
# 对当前目录下所有 .txt 扩展的文件进行字数统计
```

```bash
xz myfiles.txt
# 将文件 "myfiles.txt" 压缩为 "myfiles.txt.xz"
```

```bash
xz -dk myfiles.txt.xz
# 将 "myfiles.txt.xz" 解压为 "myfiles.txt"
```

```bash
mkdir -m a=rwx dir
# 创建目录 "dir" 并设置其文件模式，允许所有用户读、写、执行
```

```bash
modinfo snd
# 显示关于 Linux 内内核模块 "snd"的所有可用信息
```

```bash
more +3 myfiles.txt
# 从第3行开始显示文件 "myfiles.txt" 的内容
```

```bash
more +/"Hello" myfiles.txt
# 从文件 "myfiles.txt"包含字符串 "Hello"的第一行开始显示内容
```

```bash
netstat -g
# 显示 IPv4 和 IPv6 的组播组组成信息
```

```bash
netstat -c
# 每隔几秒打印一次 netstat 信息
```

```bash
netstat -natp
# 显示活动 Internet 连接的统计信息
```

```bash
netstat -rn
# 显示绑定到服务器的所有 IP 地址的路由表
```

```bash
netstat -an
# 显示指向服务器的所有活动连接的信息
```

```bash
od -b myfiles.txt
# 以八进制格式显示 "myfiles.txt" 的内容
```

```bash
od -Ax -c myfiles.txt
# 以 ASCII 字符格式显示 "myfiles.txt" 的内容 - 以十六进制显示字节偏移量
```

```bash
trap -l
# 显示信号名称及其对应数字的列表
```

```bash
trap
# 显示当前设置的信号陷阱列表
```

```bash
yum list openssh
# 搜索名为 "OpenSSH" 的软件包
```

```bash
yum grouplist
# 列出所有可用的组包
```

```bash
yum repolist
# 列出所有启用的 Yum 仓库
```

```bash
yum repolist all
# 列出所有已启用和禁用的 Yum 仓库
```

```bash
paste 1.txt 2.txt
# 并排显示 1.txt 和 2.txt 的内容
```

```bash
ls -a | pr -n -h "Files in $(pwd)" > dc.txt
```

```bash
cat dc.txt
```
