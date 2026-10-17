
# Linux 编程入门指南：逐章详解

## 专家洞察

超越 Linux 编程的基础知识，探索如何：

- 为你的 Linux 应用程序构建并定制 GUI 环境
- 发挥 X Window 系统以及 KDE 和 GNOME 库的威力
- 精通系统编程主题，包括进程、信号、内存管理和进程间通信
- 将网络功能集成到你的 Linux 应用程序中

## 权威建议

`Linux` 顾问 `Kurt Wall` 专注于 `Linux` 上的 `Informix` 数据库开发，并维护 `Informix on Linux` 常见问题解答（FAQ）。`Mark Watson` 是 `Intelligenesis` 公司的资级 AI 工程师，拥有十余部著作。

## 全面的解决方案

# Linux 编程

`Kurt Wall`, `Mark Watson`, 和 `Mark Whitis`

`Cindy Fields`

`Jason R.Wright`

`Tim Osborn`

引言 1

# Linux 编程实战

- 外部外设 30
- 打印机 30
- 扫描仪 32
- 数码相机 32
- 居家自动化 33
- 完整系统 33
- 笔记本电脑 34
- 安装 34
- 总结 38
- 使用 GNU cc 39
- GNU cc 的特性 40
- 简短教程 40
- 常用命令行选项 43
- 库文件与包含文件 44
- 错误检查与警告 45
- 优化选项 47
- 调试选项 48
- GNU C 扩展 49
- 总结 51
- 使用 GNU make 进行项目管理 53
- 为什么用 make? 54
- 编写 Makefile 54
- 关于规则的更多信息 56
- 伪目标 (Phony Targets) 56
- 变量 57
- 环境、自动和预定义变量 59
- 隐式规则 60
- 模式规则 61
- 注释 61
- 额外的 make 命令行选项 61
- 调试 make 62
- 常见的 make 错误信息 63
- 有用的 Makefile 目标 63
- 总结 64
- 使用 autoconf 创建自自配置软件 75
- 理解 autoconf 66
- 构建 configure.in 67
- 文件结构化 68
- 有帮助的 autoconf 工具 69
- 内置宏 69
- 替代程序的测试 69
- 库函数测试 70
- 头文件测试 71
- 结构体测试 72
- typedef 测试 73
- 编译器行为测试 73
- 系统服务测试 74
- UNIX 变体测试 75
- 通用宏 76
- 一个带注释的 autoconf 脚本 77
- 总结 83

## 6 比较与合并源文件 85

- 比较文件 86
- 理解 `cmp` 命令 86
- 理解 `diff` 命令 88
- 理解 `diff3` 命令 95
- 理解 `sdiff` 命令 98
- 准备源代码补丁 98
- `patch` 命令行选项 98
- 创建补丁 100
- 应用补丁 100
- 总结 101

## 7 使用 RCS 进行版本控制 103

- 术语 104
- RCS 基础用法 105
- `ci` 和 `co` 105
- RCS 关键字 107
- `t` 命令 109
- `rcdiff` 110
- 其他 RCS 命令 113
- `rcslean` 113
- `rclog` 113
- `rcs` 114
- `rcsmerge` 114
- 总结 114

## 8 在 Emacs 中创建程序 115

- Emacs 简介 116
- 启动与停止 Emacs 117
- 移动 119

# Linux 编程实战

- 插入文本 120
- 删除文本 120
- 查找与替换 121
- 保存与打开文件 123
- 多窗口 124
- 支持编程的特性 125
- 缩进便利 125
- 语法高亮 126
- 使用注释 126
- 编译 Emacs 127
- 简述自定义 130
- 使用 Emacs Lisp 自动化 Emacs 132
- 总结 134
- 文件描述符 138
- 使用文件描述符的调用 138
- `open()` 调用 139
- `close()` 调用 140
- `read()` 调用 140
- `write()` 调用 140
- `ioctl()` 调用 141
- `fcntl()` 调用 141
- `fsync()` 调用 142
- `ftruncate()` 调用 142
- `lseek()` 调用 143
- `dup()` 调用与 `dup2()` 调用 143
- `select()` 调用 144
- `fstat()` 调用 149
- `fchown()` 调用 149
