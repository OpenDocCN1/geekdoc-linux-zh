
## 设置声音和多媒体

简介

获取声音

Linux 内核声音

初始手动配置

自动加载模块

ISA PnP 卡

最终 PnP 步骤——使 PnP 设置永久化

OSS—开放声音系统

OSS 下载与安装

OSS 配置技巧及行业新闻

配置 SoftOSS

ALSA——高级 Linux 声音架构

安装 ALSA

测试 ALSA

在启动时加载 ALSA

音频数据操作与转换

提取数字音频数据

技术细节

cdparanoia

MPEG 1 Layer 3 编码

MP3——使用与误用

MP3 归档

bladenc

使用 shorten 进行无损音频编码

shorten——从哪里获取

shorten——如何使用

SoundTraker 模块

libkmikmod

测试 libkmikmod

MIDI 简介

通用 MIDI 系统

MIDI 乐器——FM 与波表合成

软件 MIDI 合成

SoftOSS

Kmid3

TiMidity++

为 TiMidity++ 和 OSS 安装补丁文件

后续步骤

## 第四部分 编程、自动化与内核编译

### 30 Shell 和 awk 编程

- 使用 bash 进行 Shell 编程
- bash 变量
- 环境变量
- Shell 脚本
- 条件结构
  - if 语句
  - case 语句
- 循环结构
  - while 和 until 语句
  - for 语句
- 内置 Shell 变量和位置参数
- 函数
- 深入 Shell 编程
- awk 脚本
  - awk 模式
  - 记录和字段
  - 调用 awk
  - 更改字段分隔符
  - 赋值变量值
  - 内置 awk 变量
  - 数组
  - awk 表达式
- 控制语句
  - if 语句
  - while 语句
  - do 语句
  - for 语句
  - break 和 continue 语句
  - delete 语句
  - exit 语句
- I/O 语句
- 内置函数
- 用户定义函数
- 深入 awk
- 总结

### 31 配置和构建内核

- 为什么要重新构建内核？
- 模块与集成驱动
- 构建内核
- 配置内核
  - 代码成熟度级别选项
  - 处理器类型和功能
  - 可加载模块支持
  - 通用设置
  - 即插即用支持
  - 块设备
  - 网络选项
  - SCSI 支持
    - SCSI 低级驱动程序
  - 网络设备支持
  - 业余无线电支持
  - IrDA 子系统支持
    - 红外端口设备驱动程序
  - ISDN 子系统
  - 旧 CD-ROM 驱动程序
  - 字符设备
    - 鼠标
    - 用于 Linux 的视频
    - 摇杆支持
    - Fjape
  - 文件系统
  - 网络文件系统
  - 分区类型
  - 本地语言支持
  - 控制台驱动程序
  - 声音
  - 通用串行总线
  - 内核黑客调试
- 编译内核
  - 生成依赖项
  - 构建内核
  - 构建模块
  - 安装模块
  - 安装内核
- 总结

## 第五部分 开发环境

### 32 Perl 编程

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
- 条件语句：if/else 和 unless
  - if
  - unless
- 循环
  - for
  - foreach
  - while
  - until
  - last 和 next
  - do...while 和 do...until
- 正则表达式
- 访问 Shell
- 开关
- 模块和 CPAN
- 代码示例
  - 发送邮件
  - 清除日志
  - 发布到 Usenet
  - 单行程序
- 命令行处理
- Perl 相关工具
- 更多信息
  - 书籍
  - Usenet
  - WWW
  - 其他
- 总结

### 33 Tcl/Tk 简介

- 快速示例
- Tk 中的“你好，世界”
- Tcl 语法和概念
  - 变量替换
  - 命令替换
  - 反斜杠替换
  - 引号
  - 注释
  - 变量
  - 数组
  - 表达式
    - 数字
    - 运算符
    - 内置函数
  - 列表
    - 提取列表元素
    - 创建列表
    - 操作列表
    - 列表和命令
  - 控制结构
    - if
    - while
    - for
    - foreach
    - break 和 continue
    - switch
    - source
    - eval
  - 过程
    - proc
    - 局部和全局变量
    - 参数
- Tk
  - 小部件
- Tcl 扩展
- 深入探索
- 总结

### 34 Python 简介

- 简介
  - pulpipush
  - 运行 pulpish
- 什么是 Python？
- 优势
- 快速上手
- 基础
  - 数值对象概述
  - 字符串和字符串转换概述
- 编写 Python 脚本
- Python 的强大之处
  - 列表处理能力
  - 列表处理运算符
  - 更多序列类型
    - 字符串的可变性
    - 列表的可变性
    - del 语句
    - 值 None
    - 排序列表
    - 元组
    - 字典
- 比较和循环结构
  - 比较
  - 循环结构
  - 循环控制语句
- 函数和命名空间
  - 函数描述
  - 返回值
  - 命名空间简介
  - 命名空间混淆——全局救场
- 输入和输出
  - 输入
  - 输出
- OS 模块、函数和方法
- 异常
  - try...except
  - try...finally
  - 大量异常
- 现实世界：示例代码
  - 示例：图形目录列表
- Python 强力工具：嵌入式 Python
  - 使用嵌入式 Python 在 HTML 代码中插入时间戳
- 面向对象编程
  - OOP 简介——如何避免混淆
  - 类定义
  - 特殊方法演示——健谈对象
- 标准模块概述
  - sys 模块
  - types 模块
  - string 模块
  - math 模块
  - time 模块
  - shutil 模块
  - commands 模块
- 后续步骤
  - http://www.python.org
  - 继续教育
- 总结

### 35 C 和 C++ 简介

- C 的历史
- C 中的“你好，世界”
- 注释
  - 包含头文件
  - 主函数
- 数据类型
  - 声明变量
  - 变量作用域
  - 变量存储类别
- 语句
  - 声明
  - 定义
  - 表达式语句
  - if 语句
  - switch 语句
  - while 语句
  - do 语句
  - for 语句
  - return 语句
- 函数
- 数组、结构体和指针
  - 数组
  - 结构体
  - 指针

