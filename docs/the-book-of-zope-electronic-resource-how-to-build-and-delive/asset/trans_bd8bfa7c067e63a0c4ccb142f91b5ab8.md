

# ZOPE 之书
如何构建与交付 Web 应用

![](img/43a28cce5475b2f487bf455365567fb6_0_0.png)

Beehive

LINUX JOURNAL PRESS

拒绝分化，拒绝刻板教条！！

# ZOPE 之书

![](img/43a28cce5475b2f487bf455365567fb6_3_0.png)

http://archive.org/details/isbn_9781886411579-

# ## ZOPE 之书

如何构建与交付 Web 应用

beehive

Casey Duncan，技术编辑

![](img/43a28cce5475b2f487bf455365567fb6_4_0.png)

No Starch Press, Inc. 旗下品牌
旧金山

# ZOPE 之书。版权所有 ©2001 由 dpunkt.verlag GmbH。

保留所有权利。未经版权所有者和出版者的事先书面许可，不得以任何形式或任何手段（电子或机械，包括复印、录制或通过信息存储或检索系统）复制或传输本书的任何部分。

印于加拿大

1 2 3 4 5 6 7 8 9 10-04 03 02 01

本书中使用了商标名称。我们并没有在每次出现商标名称时都使用商标符号，而是仅以编辑的方式使用这些名称并为了商标所有者的利益，无侵犯商标之意。

联合出版：William Pollock 和 Paul Hughes
编辑总：Karol Jurado
助理编辑：Nick Hoff
技术编辑：Casey Duncan
封面及内页设计：Octopodus Studios

排版：Michele O'Hagan
文字编辑：Carol Lombardi
校对：Karla Maree
索引：Nancy Humphreys

《Zope 之书》是 ZOPE: Content-Management & Web-Application-Server 的英文版，该德版出版于德国，版权所有 ©2001 dpunkt.verlag GmbH。英文译本由 Jody Byrne 准备。

由 Publishers Group West 在美国书界分销，地址：1700 Fourth Street, Berkeley, CA 94170；电话：800-778-3123；传真：510-528-3444。

由 Jacqueline Gross & Associates, Inc. 在加拿大书界分销，地址：One Atlantic Avenue, Suite 105, Toronto, Ontario M6K 3E7 Canada；电话：416-531-6737；传真：416-531-4259。

如需美国和加拿大以外的贸易或分销商信息，请直接联系 No Starch Press：

No Starch Press, Inc.
555 De Halo Street, San Francisco, CA 94107
电话：415-863-9900；传真：415-863-9950；info@nostarch.com; http://www.nostarch.com

书中的信息按“现状”分发，不提供任何保证。虽然在准备本书时已采取一切预防措施，但作者或 No Starch Press, Inc. 对因书中包含的信息直接或间接导致的任何损失或损害不对任何个人或实体承担任何责任。

图书分类索引数据

+   Zope. 英语。
The book of Zope / Beehive; Jody Byrne 译。
p. cm.
包含索引。
ISBN 1-886411-57-3 (纸本)。
1. Zope (计算机文件) 2. 网站开发-计算机程序。3. 互联网编程-计算机程序。
I. Beehive (互联网服务提供商) II. 。
TK105.8885.Z66 207 2001
005.7'13769-dc21

# 目录

# 前言

# 第 8 章
Role.py 和 User.py 模块的一些方法

# 第 1 章
Zope 基础 5

# 第 9 章
ZClasses 157

# 第 2 章
快速入门 17

# 第 10 章
使用 ZClass 179

# 第 3 章
导航 Zope 39

# 第 11 章
ZCatalog 205

# 第 4 章
DTML 61

# 第 12 章
Zope 与 MySQL 229

# 第 5 章
操作 Zope 版本 103

# 第 13 章
编程 Zope：极速上手 Python 249

# 第 6 章
用户、角色与安全 111

# 第 14 章
用 Python 编写 Zope  263

# 第 7 章
本地角色与权限 129

# 第 15 章
Zope 产品 281

# 附录 C
网站产品的源码
359

# 第 16 章
调试
309

# 附录 D
一些 ZCatalog 模块方法
373

# 第 17 章
外部数据访问
323

# 附录 E
术语表
379

# 附录 A
DTML 和内置属性
333

# 索引
383

# 附录 B
REQUEST 对象
355

# 详细内容

# 前言

+   本书对象是谁？1
本书涵盖了什么？1
如何使用本书 2
具备 HTML 知识的 Zope 用户 2
具备 HTML 和 Python 知识的 Zope 用户 2
没有 Zope 知识的高级 Zope 用户 2
Zope 来自何？3
关于作者 3

# 1 ZOPE 基础

+   1.1 Web 应用 5
1.1.1 开发者的优势 6
1.2 作为 Web 应用服务器 6
1.2.1 按内容 7
1.2.2 SQL 语言 7
1.2.3 Python 7
1.3 内容管理 7
1.4 技术要求 8
1.5 安装 8
1.5.1 Windows 10
1.5.2 Windows NT 11
1.5.3 Linux 16
总结

# 2 快速入门

+   2.1 准备 17
2.1 创建账户 18
2.2 Zope 界面 19
2.2.1 左侧框架 20
2.2.2 右侧框架 21
2.3 Zope 对象编程 22
2.3.1 创建文件夹 23
2.3.2 创建文件 24
2.3.3 DTML 方法 25
2.3.4 创建 DTML 文档 26
2.4 管理对象 27
2.4.1 Zope 28
2.4.2 复制对象 29
2.4.3 删除对象 30
2.4.4 移动对象 31
2.5 Zope 对象 32
2.5.1 33
总结

# 3 导航 ZOPE

+   3.1 ZCatalog 39
3.1.1 内容 40
3.1.2 屏幕 41
3.1.3 帮助 42
3.1.4 撤销 43
3.2 控制 44
3.2.1 关 45
3.2.2 重启 46
3.2.3 数据库 47
3.2.4 你的数据库 48
3.2.5 恢复你的数据库 49
3.2.6 Zope 50
3.2.7 管理 51
总结

# 4 DTML

+   4.1 基础 61
4.1.1 第一、第二、第三个标签 62
4.1.2 非空对象 63
4.2 DTML 64
4.2.1 空 65
4.2.2 语法 66
4.2.3 属性 67
4.3 DTML 与属性 68
4.3.1 变量 69
4.3.2 服务器 70
4.3.3 Python 71
4.3.4 if 72
4.3.5 elif 73
4.3.6 unless 74
4.3.7 for 75
4.3.8 and 76
4.3.9 with 77
4.3.10 in 78
4.3.11 or 79
4.3.12 define 80
4.3.13 try 81
4.3.14 except 82
4.3.15 catch 83
4.3.16 finally 84
4.3.17 raise 85
4.3.18 return 86
4.3.19 break 87
4.3.20 continue 88
4.3.21 insert 89
4.3.22 delete 90
4.3.23 update 91
4.3.24 select 92
4.3.25- 93
4.3.26- 94
4.3.27- 95
4.3.28 with 96
4.3.29 with 97
4.3.30 with 98
4.3.31 with 99
4.3.32 with 100
4.3.33 with 101
4.3.34 with 102
4.3.35 with 103
4.3.36 with 104
4.3.37 with 105
4.3.38 with 106
4.3.39 with 107
4.3.40 with 108
4.3.41 with 109
4.3.42 with 110
总结

# 5 操作 ZOPE 版本

+   5.1 创建 Zope 版本 103
5.2 升级 Zope 版本 104
5.3 安装 Zope 版本 105
5.4 降级 Zope 版本 106
5.5 管理 Zope 版本 107
5.6 备份 Zope 版本 108
5.7 恢复 Zope 版本 109
总结

# 6 用户、角色与安全

+   6.1 Zope 安全 111
6.1.1 安全模型 112
6.1.2 用户 113
6.1.3 角色 114
6.1.4 权限 115
6.1.5 组 116
6.2 认证 117
6.2.1 基础认证 118
6.2.2 数据库认证 119
6.2.3 LDAP 认证 120
6.3 授权 121
6.3.1 基于角色的授权 122
6.3.2 访问控制列表 123
总结

# 7 本地角色与权限

+   7.1 本地角色 129
7.1.1 示例 130
7.2 代理角色 131
7.3 权限 132
7.3.1 非文件夹对象的权限 133
7.3.2 文件夹对象的权限 135

