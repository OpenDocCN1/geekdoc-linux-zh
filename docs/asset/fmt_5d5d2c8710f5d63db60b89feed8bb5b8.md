
# BTFM：蓝队实战手册

## 前言

BTFM 命令行语法：

| 符号 | 说明 |
| --- | --- |
| `#` | 通用 Linux/*n shell 提示符，sudo 也可以配合 `$` 使用 |
| `C:\>` | Windows 提示符，可能需要管理员权限 CMD 提示符 |
| `PS C:\>` | Windows PowerShell |
| `>` | 通用提示符，多操作系统 |
| `<IP ADDRESS>`, `<PORT>`, `<USER>`, `<PASSWORD>`, 等 | 需要用户确定输入并移除 `<>` 括号 |
| `–` | 注意复制/粘贴时使用破折号/连字符 (en/em/dash ,,- hyphen –) |
| `spaces` | 确保检查检查命令中有空格和无空格的地方。 |

更新、编辑和补充材料：

参考 <http://www.bluetefieldmanual.com>

BTFM 基于 NIST 网络安全框架：

参考 <http://www.nist.gov/cyberframework/>

## 目录

- TCPDUMP
- TSHARK
- SNORT
- 网络捕获 (PCAP) 工具
  - EDITCAP
  - MERGECAP
- 蜜罐技术
  - WINDOWS
  - LINUX
- NETCAT
- 被动 DNS 监控
- 日志审计
  - WINDOWS
  - LINUX

## 4 响应（分析）

### 现场分查 - WINDOWS

- 系统信息
- 用户信息
- 网络信息
- 服务信息
- 策略、补丁和设置信息
- 自启动和自动加载信息
- 日志
- 文件、驱动器和共享信息

### 现场分查 - LINUX

- 系统信息
- 用户信息
- 网络信息
- 服务信息
- 策略、补丁和设置信息
- 日志
- 文件、驱动器和共享信息

### 恶意软件分析

- 静态分析基础
- 识别恶意软件
- 进程管理器
- 文件哈希分析
- 哈希查询
- 硬盘和内存取证
  - WINDOWS
  - LINUX

## 5 恢复（修复）

### 补丁

- WINDOWS
- LINUX

### 备份

- WINDOWS
- LINUX

### 杀死恶意软件进程

- WINDOWS
- LINUX

### OS 秘籍

- WINDOWS
- LINUX

### 解码

### 进制转换

### SNORT

- SNORT 规则

### DOS/DDOS

- 指纹识别 DOS/DDOS

### 工具工具

### 预构建、虚拟机和发行版

### 应急响应清单

- 识别任务
- 遏制任务
- 修复任务
- 其他 / 经验总结任务
- 恶意软件属性清单

### 事件记录与事件共享词汇 (VERIS)

- 概述
- 攻击者
- 行为
- 资产
