
```
=> ufw allow 23
=> ufw reload
```

`[ufw]` 是用于 ubuntu/debian 服务器的防火墙

[默认禁用 root 登录]

服务器端配置到此

# 安装 Telnet 客户端 (Ubuntu)

## 第 1 步

- 1) 安装 telnet 客户端

```
=> apt install telnet -y
```

## 第 2 步

- 2) 连接到系统

```
=>telnet <server_ip_address>
```

示例：

# UBUNTU $ CENTOS 管理员

```
=>telnet 192.168.0.100
```

***

# 磁盘管理

硬盘提供空间。在使用硬盘之前，我们必须将其划分为若干部分。它可以只是一个巨大的部分（意味着一个分区），也可以被划分为多个部分（多个分区）。例如，我们可以将其划四个主分区，如果想划分更多，可以使用带有不同大小的扩展分区。每个分区后都可以进行格式化，以便 Windows 识别它，另一个可以格式化为 Linux 格式，等等。每个单独的部分都作为一个文件系统工作，其中存储不同的数据，我们可以对其操作。要操作分区，我们插入一个驱动器。我们可以物理地这样做，如果你在虚拟机上，可以添加空白硬盘。添加硬盘（物理或虚拟）后，我们可以通过此命令显示状态

```
=>sudo fdisk -l
```

要查看块设备，可以使用命令

```
=>lsblk
```

对于我的电脑，我添加了两个虚拟硬盘，所以

# UBUNTU $ CENTOS 管理员

我的电脑结果如下：

```
[vagrant@localhost ~]$ lsblk
NAME               MAJ:MIN RM RO TYPE
sda               8:0    0 9.9G 0 disk
  ├sda1             8:1    0 500M 0 part /boot
  └─sda2            8:2    0 9.4G 0 part
      ├─centos-root 253:0  0 8.4G 0 svm /
      └─centos-swap 253:1  0 1016M 0 svm
[SWAP]
sdb               8:16   0 30G 0 disk
sdc               8:32   0 30G 0 disk
sr0               11:0   1 1024M 0 rom
sr1               11:1   1 1024M 0 rom
```

所以我们有块设备 `sdb` 和 `sdc`，都是 30 GB，而且它们是完全空的。它们只是原始磁盘。所以这些是尚未进行任何分区的块设备。表格中的交换 分区作为虚拟内存来支持内存，在内存不足的情况下，它可以帮助防止内存溢出。在块设备中创建分区的命令是：

```
=> sudo fdisk /dev/sdb
```

然后查看命令，我们需要输入 `'m'`

# 命令 (m 获取帮助): m

命令操作

a 切换启动项

b 打印分区

c 显示分区

d 删除分区

e 使用扩展分区

f 打印分区表

g 创建 GPT 分区表

h 交互式帮助

i 忽略签名

j 更改签名类型

m 帮助

n 新分区

o 创建主分区表

p 打印分区表

q 退出不保存更改

r 标记扇区

s 切换类型

t 更改分区类型

u 更改系统标识

v 显示分区表并退出

x 退出不保存更改

y 写入更改并退出

z 退出并重置

分区类型列表：

7 Linux

8 Linux-swap

8e LVM

9 HP-Linux

81 NTFS

82 Linux9

82 Linux

83 Solaris

84 Solaris

85 Solaris

86 Linux

17 Linux

18 Linux

19 Linux

20 Linux

21 Linux

22 Linux

23 Linux

24 Linux

25 Linux

26 Linux

27 Linux

28 Linux

29 Linux

30 Linux

31 Linux

32 Linux

33 Linux

34 Linux

35 Linux

36 Linux

37 Linux

38 Linux

39 Linux

40 Linux

41 Linux

42 Linux

43 Linux

44 Linux

45 Linux

46 Linux

47 Linux

48 Linux

49 Linux

50 Linux

51 Linux

52 Linux

53 Linux

54 Linux

55 Linux

56 Linux

57 Linux

58 Linux

59 Linux

60 Linux

61 Linux

62 Linux

63 Linux

64 Linux

65 Linux

66 Linux

67 Linux

68 Linux

69 Linux

70 Linux

71 Linux

72 Linux

73 Linux

74 Linux

75 Linux

76 Linux

77 Linux

78 Linux

79 Linux

80 Linux

81 Linux

82 Linux

83 Linux

84 Linux

85 Linux

86 Linux

87 Linux

88 Linux

89 Linux

90 Linux

91 Linux

92 Linux

93 Linux

94 Linux

95 Linux

96 Linux

97 Linux

98 Linux

99 Linux

a 0 Linux

a 1 Linux

a 2 Linux

a 3 Linux

a 4 Linux

a 5 Linux

a 6 Linux

a 7 Linux

a 8 Linux

a 9 Linux

a a Linux

a b Linux

a c Linux

a d Linux

a e Linux

a f Linux

a g Linux

a h Linux

a i Linux

a j Linux

a k Linux

a l Linux

a m Linux

a n Linux

a o Linux

a p Linux

a q Linux

a r Linux

a s Linux

a t Linux

a u Linux

a v Linux

a w Linux

a x Linux

a y Linux

a z Linux

b 0 Linux

b 1 Linux

b 2 Linux

b 3 Linux

b 4 Linux

b 5 Linux

b 6 Linux

b 7 Linux

b 8 Linux

b 9 Linux

b a Linux

b b Linux

b c Linux

b d Linux

b e Linux

b f Linux

b g Linux

b h Linux

b i Linux

b j Linux

b k Linux

b l Linux

b m Linux

b n Linux

b o Linux

b p Linux

b q Linux

b r Linux

b s Linux

b t Linux

b u Linux

b v Linux

b w Linux

b x Linux

b y Linux

b z Linux

c 0 Linux

c 1 Linux

c 2 Linux

c 3 Linux

c 4 Linux

c 5 Linux

c 6 Linux

c 7 Linux

c 8 Linux

c 9 Linux

c a Linux

c b Linux

c c Linux

c d Linux

c e Linux

c f Linux

c g Linux

c h Linux

c i Linux

c j Linux

c k Linux

c l Linux

c m Linux

c n Linux

c o Linux

c p Linux

c q Linux

c r Linux

c s Linux

c t Linux

c u Linux

c v Linux

c w Linux

c x Linux

c y Linux

c z Linux

d 0 Linux

d 1 Linux

d 2 Linux

d 3 Linux

d 4 Linux

d 5 Linux

d 6 Linux

d 7 Linux

d 8 Linux

d 9 Linux

d a Linux

d b Linux

d c Linux

d d Linux

d e Linux

d f Linux

d g Linux

d h Linux

d i Linux

d j Linux

d k Linux

d l Linux

d m Linux

d n Linux

d o Linux

d p Linux

d q Linux

d r Linux

d s Linux

d t Linux

d u Linux

d v Linux

d w Linux

d x Linux

d y Linux

d z Linux

e 0 Linux

e 1 Linux

e 2 Linux

e 3 Linux

e 4 Linux

e 5 Linux

e 6 Linux

e 7 Linux

e 8 Linux

e 9 Linux

e a Linux

e b Linux

e c Linux

e d Linux

e e Linux

e f Linux

e g Linux

e h Linux

e i Linux

e j Linux

e k Linux

e l Linux

e m Linux

e n Linux

e o Linux

e p Linux

e q Linux

e r Linux

e s Linux

e t Linux

e u Linux

e v Linux

e w Linux

e x Linux

e y Linux

e z Linux

f 0 Linux

f 1 Linux

f 2 Linux

f 3 Linux

f 4 Linux

f 5 Linux

f 6 Linux

f 7 Linux

f 8 Linux

f 9 Linux

f a Linux

f b Linux

f c Linux

f d Linux

f e Linux

f f Linux

f g Linux

f h Linux

f i Linux

f j Linux

f k Linux

f l Linux

f m Linux

f n Linux

f o Linux

f p Linux

f q Linux

f r Linux

f s Linux

f t Linux

f u Linux

f v Linux

f w Linux

f x Linux

f y Linux

f z Linux

g 0 Linux

g 1 Linux

g 2 Linux

g 3 Linux

g 4 Linux

g 5 Linux

g 6 Linux

g 7 Linux

g 8 Linux

g 9 Linux

g a Linux

g b Linux

g c Linux

g d Linux

g e Linux

g f Linux

g g Linux

g h Linux

g i Linux

g j Linux

g k Linux

g l Linux

g m Linux

g n Linux

g o Linux

g p Linux

g q Linux

g r Linux

g s Linux

g t Linux

g u Linux

g v Linux

g w Linux

g x Linux

g y Linux

g z Linux

h 0 Linux

h 1 Linux

h 2 Linux

h 3 Linux

h 4 Linux

h 5 Linux

h 6 Linux

h 7 Linux

h 8 Linux

h 9 Linux

h a Linux

h b Linux

h c Linux

h d Linux

h e Linux

h f Linux

h g Linux

h h Linux

h i Linux

h j Linux

h k Linux

h l Linux

h m Linux

h n Linux

h o Linux

h p Linux

h q Linux

h r Linux

h s Linux

h t Linux

h u Linux

h v Linux

h w Linux

h x Linux

h y Linux

h z Linux

i 0 Linux

i 1 Linux

i 2 Linux

i 3 Linux

i 4 Linux

i 5 Linux

i 6 Linux

i 7 Linux

i 8 Linux

i 9 Linux

i a Linux

i b Linux

i c Linux

i d Linux

i e Linux

i f Linux

i g Linux

i h Linux

i i Linux

i j Linux

i k Linux

i l Linux

i m Linux

i n Linux

i o Linux

i p Linux

i q Linux

i r Linux

i s Linux

i t Linux

i u Linux

i v Linux

i w Linux

i x Linux

i y Linux

i z Linux

j 0 Linux

j 1 Linux

j 2 Linux

j 3 Linux

j 4 Linux

j 5 Linux

j 6 Linux

j 7 Linux

j 8 Linux

j 9 Linux

j a Linux

j b Linux

j c Linux

j d Linux

j e Linux

j f Linux

j g Linux

j h Linux

j i Linux

j j Linux

j k Linux

j l Linux

j m Linux

j n Linux

j o Linux

j p Linux

j q Linux

j r Linux

j s Linux

j t Linux

j u Linux

j v Linux

j w Linux

j x Linux

j y Linux

j z Linux

k 0 Linux

k 1 Linux

k 2 Linux

k 3 Linux

k 4 Linux

k 5 Linux

k 6 Linux

k 7 Linux

k 8 Linux

k 9 Linux

k a Linux

k b Linux

k c Linux

k d Linux

k e Linux

k f Linux

k g Linux

k h Linux

k i Linux

k j Linux

k k Linux

k l Linux

k m Linux

k n Linux

k o Linux

k p Linux

k q Linux

k r Linux

k s Linux

k t Linux

k u Linux

k v Linux

k w Linux

k x Linux

k y Linux

k z Linux

l 0 Linux

l 1 Linux

l 2 Linux

l 3 Linux

l 4 Linux

l 5 Linux

l 6 Linux

l 7 Linux

l 8 Linux

l 9 Linux

l a Linux

l b Linux

l c Linux

l d Linux

l e Linux

l f Linux

l g Linux

l h Linux

l i Linux

l j Linux

l k Linux

l l Linux

l m Linux

l n Linux

l o Linux

l p Linux

l q Linux

l r Linux

l s Linux

l t Linux

l u Linux

l v Linux

l w Linux

l x Linux

l y Linux

l z Linux

m 0 Linux

m 1 Linux

m 2 Linux

m 3 Linux

m 4 Linux

m 5 Linux

m 6 Linux

m 7 Linux

m 8 Linux

m 9 Linux

m a Linux

m b Linux

m c Linux

m d Linux

m e Linux

m f Linux

m g Linux

m h Linux

m i Linux

m j Linux

m k Linux

m l Linux

m m Linux

m n Linux

m o Linux

m p Linux

m q Linux

m r Linux

m s Linux

m t Linux

m u Linux

m v Linux

m w Linux

m x Linux

m y Linux

m z Linux

n 0 Linux

n 1 Linux

n 2 Linux

n 3 Linux

n 4 Linux

n 5 Linux

n 6 Linux

n 7 Linux

n 8 Linux

n 9 Linux

n a Linux

n b Linux

n c Linux

n d Linux

n e Linux

n f Linux

n g Linux

n h Linux

n i Linux

n j Linux

n k Linux

n l Linux

n m Linux

n n Linux

n o Linux

n p Linux

n q Linux

n r Linux

n s Linux

n t Linux

n u Linux
