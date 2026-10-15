

# UNIX 安全

使用经过验证的方法管理安全的 UNIX 系统

- 安全的网络连接
- 远程密码更新
- 限制机器访问
- 登录监控
- 构建防火墙
- 检查用户安全
- 协调密码和组文件
- 自动化网络维护
- 管理超级用户权限
- 超时空闲用户
- 以及更多

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_0_0.png)

# UNIX 安全

系统管理员
核心参考系列

R&D Books
Lawrence, KS 66046

R&D Books
1601 West 23rd Street, Suite 200
Lawrence, Kansas 66046
USA

公司用来区分其产品的名称通常被声明为商标。在所有 R&D 知晓商标声明的情况下，产品名称均以首字母大写、全部大写或根据供应商的大小写偏好显示。读者应联系相关公司以获取有关商标和商标注册的更完整信息。本书中的所有商标和注册商标均为其各自持有者的财产。

Copyright © 1997 by Miller Freeman, Inc., except where noted otherwise. Published by R&D Books, an imprint of Miller Freeman, Inc. All rights reserved. Printed in the United States of America. No part of this publication may be reproduced or distributed in any form or by any means, or stored in a database or retrieval system, without the prior written permission of the publisher; with the exception that the program listings may be entered, stored, and executed in a computer system, but they may not be reproduced for publication.

本书中的程序仅用于教学目的。程序经过仔细测试，但不保证任何特定用途。出版商不提供任何保证，也不保证此处信息的准确性、充分性或完整性，且不对因使用本信息而产生的任何错误或遗漏负责。出版商不对因使用本信息而导致的对第三方知识产权的任何侵权或由此产生的任何损害承担责任。

**Distributed in the U.S. and Canada by:**
**Publishers Group West**
**P.O. Box 8843**
**Emeryville, CA 94662**
**ISBN: 0-87930-471-5**

![](img/113bcc15fc2db8f0f40ac5d1e755f41c_3_0.png)

# 目录

- Chapter 1  Assorted Security Tips for UNIX ........ 1
- Tip 1: Know Your Network ....................... 2
- Tip 2: Keep Close Watch on Your Network ........ 2
- Tip 3: Decide What You Want to Protect ......... 3
- Tip 4: Establish a Workable Security Policy. ..... 3
- Tip 5: Know Thy TCP/IP....................... 4
- Tip 6: Enable Only What You Need ............... 8
- Tip 7: Accept Only Trusted Hosts
  (from Trusted Interfaces)....................... 9
- Tip 8: Log and Scan as Much as You Can ......... 10
- Tip 9: Watch the Security Mailing Lists
  on the Internet ............................... 11
- Tip 10: Always Test a Password Scheme
  before Implementing It ....................... 11
- Conclusion................................... 12

# Chapter 2 — Checking User Security ··············· 13

Duplicate Home Directories ······················· 14
Catching Idle Users ······························· 16
In Search of Ancient Accounts ····················· 18
Stalking the Wily Aging Report ····················· 25
Summary ··········································· 31

# Chapter 3 — Coordinating Password and
Group Files ······································· 33

# Chapter 4 — Timing Out Idle Users ················· 37

SCO’s idleout ····································· 38
Bootstrap script ··································· 38
killidle Script ···································· 41
Running killidle ··································· 45
Summary ··········································· 47

# Chapter 5 — Managing Super-User Privileges
with a Revised sudo ······························· 49

History ··········································· 50
Security Issues ···································· 53
Security Measures ································· 53
How sudo Works ····································· 54
Configurable Parameters ···························· 59
Configuration File ·································· 60
Log File ············································ 60
Using sudo ········································· 61
Enhancements ······································· 61
Conclusion ·········································· 62

