
## 23 管理 DNS

- 为客户端配置 DNS
- /etc/hosts.conf 文件
- /etc/nsswitch.conf 文件
- /etc/hosts 文件
- /etc/resolv.conf 文件
- 理解由 DHCP 所做的更改
- 基本 DNS 概念
    - 名称服务器如何存储 DNS 结构信息
    - DNS 如何向用户提供名称服务信息
    - 实际中的名称解析
- 使用 DNS 工具
    - dig
    - host
    - nslookup
    - whois
- 配置本地缓存名称服务器
- 自己的域名和第三方 DNS
- 使用 BIND 为真实域名提供 DNS 服务
    - rndc.conf
    - named.conf
    - 日志记录
    - 解析器配置
    - 运行 named 名称服务器守护进程
- 为真实域名提供 DNS 服务
    - 正向区域
    - 反向区域
    - 注册域名
- DNS 故障排除
    - 委托问题
    - 反向查找问题
    - 维护准确的序列号
    - 区域文件中的问题排查
    - 故障排除工具
        - 使用 Fedora 的 BIND 配置工具
- 管理 DNS 安全
    - UNIX 安全考量
    - DNS 安全考量
    - 使用 DNS 安全扩展
    - 使用分裂 DNS
- 参考资料

## 24 LDAP

- 配置服务器
- 填充您的目录
- 配置客户端
    - Evolution
    - Thunderbird
- 管理
- 参考资料

### 第五部分 Linux 编程

## 25 使用 Perl

- 在 Linux 中使用 Perl
- Perl 版本
- 一个简单的 Perl 程序
- Perl 变量和数据结构
    - Perl 变量类型
    - 特殊变量
- 运算符
    - 比较运算符
    - 复合运算符
    - 算术运算符
    - 其他运算符
    - 特殊字符串常量
- 条件语句
    - if/else
    - unless
- 循环
    - for
    - foreach
    - while
    - until
    - last 和 next
    - do ... while 和 do ... until
- 正则表达式
- 访问 Shell
- 模块和 CPAN
- 参考资料
- 书籍

## 26 使用 Python 进行开发

- Linux 上的 Python
    - 进入交互模式
- Python 基础
    - 数字
    - 更多关于字符串的内容
    - 列表
    - 字典
    - 条件语句和循环
- 函数
- 面向对象
    - 类和对象变量
    - 构造器和析构器
    - 类继承
    - 多重继承
- 标准库和帕纳索斯山（Vaults of Parnassus）
- 参考资料

## 27 编写 PHP 脚本

- PHP 简介
    - 进入和退出 PHP 模式
    - 变量
    - 数组
    - 常量
    - 注释
    - 转义序列
    - 变量替换
    - 运算符
    - 条件语句
    - 特殊运算符
    - 切换（Switch）
    - 循环
    - 包含其他文件
- 基本函数
    - 字符串
    - 数组
    - 文件
    - 杂项
- 处理 HTML 表单
- 参考资料

## 28 Fedora 的 C/C++ 编程工具

- 使用 Linux 进行 C/C++ 编程
- 使用 Fedora Linux 提供的 C 编程项目管理工具
    - 使用 make 构建程序
    - 使用 autoconf 实用工具配置代码
    - 使用 Subversion 管理软件项目
    - 调试工具
- 使用 GNU C 编译器
- 图形化开发工具
    - 使用 KDevelop 客户端
    - 用于在 GNOME 中开发的 Glade 客户端
- 参考资料

## 29 Mono

- 为什么要使用 Mono？
- 命令行中的 Mono
- C# 程序的结构
    - 打印参数
    - 创建您自己的变量
    - 添加一些错误检查
- 基于 Mono 库构建
    - 使用 Beagle 进行搜索
    - 使用 Gtk# 创建图形用户界面
- 参考资料

### 第六部分 Fedora 日常维护

## 30 保护您的机器

- 理解计算机攻击
- 评估您的易受攻击性
- 保护您的机器
    - 保护无线网络安全
    - 密码和物理安全
    - 配置和使用 Tripwire
    - 设备
- 病毒
- 配置您的防火墙
- 制定灾难恢复计划
- 关注 Linux 安全问题的最新动态
- 理解 SELinux
- 参考资料

## 31 性能调优

- 硬盘
    - 使用 BIOS 和内核调优磁盘驱动器
    - hdparm 命令
    - 文件系统调优
        - tune2fs 命令
        - e2fsck 命令
        - badblocks 命令
        - 禁用文件访问时间
- 内核
- Apache
- MySQL
    - 测量关键缓冲区使用情况
    - 使用查询缓存
    - 其他优化技巧
    - 查询优化
- 参考资料

## 32 命令行大师课

- 为什么要使用 Shell？
- 基本命令
    - 使用 cat 打印文件内容
    - 使用 cd 更改目录
    - 使用 chmod 更改文件访问权限
    - 使用 cp 复制文件
    - 使用 du 打印磁盘使用情况
    - 使用 find 通过搜索查找文件
    - 使用 grep 在输入中搜索字符串
    - 使用 less 分页显示输出
    - 使用 ln 在文件之间创建链接
    - 使用 locate 从索引中查找文件
    - 使用 ls 列出当前目录中的文件
    - 使用 man 阅读手册页
    - 使用 mkdir 创建目录
    - 使用 mv 移动文件
    - 使用 ps 列出进程
    - 使用 rm 删除文件和目录
    - 使用 tail 打印文件的最后几行
    - 使用 top 打印资源使用情况
    - 使用 which 打印命令的位置
- 组合命令
- 多个终端
- 日期和时间
    - 使用 date 命令
    - 使用 hwclock 命令
    - 捕获屏幕图像
- 参考资料
- 书籍

## 33 编写和执行 Shell 脚本

- 运行 Shell 程序
- 通过特定 Shell 解释 Shell 脚本
- 在 Shell 脚本中使用变量
    - 为变量赋值
    - 访问变量值
    - 位置参数
- 使用简单脚本自动化任务
- 内置变量
- 特殊字符
    - 使用双引号解析包含嵌入空格的字符串中的变量
    - 使用单引号保持变量未展开
    - 使用反斜杠作为转义字符
    - 使用反引号将字符串替换为输出
- bash 中的表达式比较
    - 字符串比较
    - 数字比较
    - 文件运算符
    - 逻辑运算符
- 特殊语句：for、while 及其他
    - for 语句
    - while 语句
    - until 语句
    - shift 语句
    - if 语句
    - case 语句
    - break 和 exit 语句
- 在 Shell 脚本中使用函数
- 参考资料

## 34 高级软件管理

- 使用 RPM 进行软件管理
    - 命令行上的 rpm
    - 两个实用选项

