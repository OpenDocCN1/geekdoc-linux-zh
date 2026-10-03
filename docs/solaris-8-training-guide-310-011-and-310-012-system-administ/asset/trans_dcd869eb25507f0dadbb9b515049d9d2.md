
## 应用你的知识

系统将要求你识别客户端可以从中获取名称服务信息的 NIS 服务器。输入 NIS 主服务器名称，然后按回车键。

当被要求添加下一个主机时，按 Ctrl+D。

5. 通过执行以下脚本启动 NIS 守护进程：
`/usr/lib/netsvc/yp/ypstart`

6. 通过输入以下命令验证 NIS 客户端是否已绑定到 NIS 主服务器：
`ypwhich`

应显示主服务器名称。

7. 通过注销并使用不再在本地 /etc/passwd 文件中而由 NIS 管理的登录名重新登录来测试 NIS 客户端。

## 复习问题

1. 以下哪项服务将用户、系统和应用程序在网络间通信所需的信息存储在中央位置？
- A. NIS 服务
- B. NFS 服务
- C. Automount
- D. AutoFS

2. 以下哪项不是 Solaris 名称服务？
- A. DES
- B. /etc
- C. NIS+
- D. DNS

3. 以下哪项是维护主机、用户、密码、组和 automount 映射信息的传统 UNIX 方法？
- A. DNS
- B. NIS
- C. NIS+
- D. /etc

4. NIS 管理数据库被称为：
- A. Files
- B. Tables
- C. Maps
- D. Objects

5. 服务器和客户端共享的映射集被称为：
- A. A table
- B. An object
- C. The NIS domain
- D. None of the above

6. 当向运行 NIS 的网络添加新系统时，你必须更新主服务器中的输入文件并运行：
- A. makedbm
- B. make
- C. yppush
- D. ypinit

7. 以下哪个命令用于显示 NIS 映射中的值？
- A. ypcat
- B. ypwhich
- C. ypserv
- D. ypbind

8. 以下哪个命令可用于确定哪个服务器是特定映射的主服务器？
- A. ypbind
- B. ypcat
- C. ypserv
- D. ypwhich

9. 以下哪项将 NIS 映射的新版本从 NIS 主服务器传播到 NIS 从服务器？
- A. ypinit
- B. yppush
- C. make
- D. yppoll

10. 以下哪项设置主服务器、从服务器和客户端使用 NIS？
- A. makedbm
- B. make
- C. ypinit
- D. yppush

11. 以下哪项是名称服务切换的配置文件？
- A. nsswitch.conf
- B. resolve.conf
- C. /etc/netconfig
- D. nsswitch.nis

12. 以下哪个文件中的每一行标识特定类型的网络信息，例如主机、密码和组；后面跟着一个或多个源，例如 NIS+ 表、NIS 映射、DNS 主机表或本地 /etc？
- A. resolve.conf
- B. nsswitch.conf
- C. /etc/netconfig
- D. nsswitch.nis

13. 在名称服务切换文件中，以下条目是什么意思？
hosts: nis [NOTFOUND=return] files
- A. Search the NIS map and then the local /etc/hosts file.
- B. Search only the NIS hosts table in the NIS map.
- C. Search only the local files, not the NIS files.
- D. Do not search the NIS hosts table or the local /etc/hosts file.

14. 在 Solaris 8 中可以找到哪些名称服务切换模板文件？
- A. nsswitch.files
- B. nsswitch.nis+
- C. nsswitch.nisplus
- D. nsswitch.fns

15. NIS+ 命名空间的组件被称为：
- A. Tables
- B. Objects
- C. Maps
- D. Directories

16. 以下哪项不是 NIS+ 的四个授权类之一？
- A. All
- B. Owner
- C. Group
- D. Nobody

17. NIS+ 访问权限的四种类型是什么？
- A. read, write, create, modify
- B. read, write, execute, no access
- C. read, write, delete, modify
- D. read, modify, create, destroy

18. NIS+ 中有多少个安全级别？
- A. 2
- B. 1
- C. 3
- D. 4

19. NIS+ 中默认的安全级别是哪个？
- A. 3
- B. 0
- C. 1
- D. 2

20. 以下哪项是互联网为 TCP/IP 网络提供的名称服务？
- A. DNS
- B. NIS
- C. NIS+
- D. None of the above

21. 每个服务器通过运行名为 的守护进程来实现 DNS
- A. named
- B. in.named
- C. nfsd
- D. dnsd

22. DNS 的主要任务是提供
- A. security service
- B. name-to-address resolution
- C. name service
- D. namespace services

23. 以下哪项描述了 NIS 身份验证和授权之间的区别？
- A. Authentication is checking if the information requester is a valid user on the network, and authorization determines whether the particular user is allowed to have or modify the information.
- B. Authorization is checking if the information requester is a valid user on the network, and authentication determines whether the particular user is allowed to have or modify the information.

24. 以下哪个文件中的条目决定如何获取特定类型的信息（即哪些命名服务（NIS、NIS+、DNS 等）可用于获取哪些类型的信息（主机、密码、组）以及应按什么顺序查询命名服务）？
- A. /etc/nsswitch.conf
- B. /etc/resolve.conf
- C. /etc/nsswitch.nis
- D. /etc/nsswitch.nisplus

25. Solaris 8 支持多少种名称服务？
- A. 3
- B. 4
- C. 5
- D. 6

26. 以下哪项是互联网使用的名称服务？
- A. DNS
- B. NIS
- C. NIS+
- D. DES

27. 以下哪个命令用于设置 NIS 主服务器？
- A. ypserver -m
- B. nisinits -m
- C. nisserver -m
- D. ypinit -m

## 复习问题的答案

1. A. NIS 存储有关工作站名称和地址、用户、网络本身和网络服务的信息。
2. A. DES 不是 Solaris 名称服务。
3. D. /etc 文件是维护主机、用户、密码、组和 automount 映射信息的传统 UNIX 方法。
4. C. NIS 管理数据库被称为 maps。
5. C. 服务器和客户端共享的映射集被称为 NIS 域。
6. B. 要使用新系统名称更新主服务器中的输入文件，你将执行 /usr/ccs/bin/make 命令。
7. A. 就像你使用 cat 命令显示文本文件的内容一样，你可以使用 ypcat 命令显示映射中的值。
8. D. 你可以使用 ypwhich 命令确定哪个服务器是特定映射的主服务器。
9. B. yppush 命令将 NIS 映射的新版本从 NIS 主服务器传播到 NIS 从服务器。
10. C. ypinit 命令构建并安装 NIS 数据库，并初始化 NIS 客户端（和服务器）的 ypservers 列表。
11. A. 在设置 NIS 服务时，设置名称服务切换，这涉及编辑 /etc/nsswitch.conf 文件。
12. B. /etc/nsswitch.nis 文件的每一行标识特定类型的网络信息，例如主机、密码和组；后面跟着一个或多个源，例如 NIS+ 表、NIS 映射、DNS 主机表或本地 /etc。
13. B. nsswitch.nis 模板中的以下条目：hosts: nis [NOTFOUND=return] files 表明仅搜索 NIS 映射中的 NIS 主机表。
14. A.、C. 以下模板文件可用：nsswitch.files、nsswitch.nisplus、nsswitch.nis、nsswitch.dns 和 nsswitch.ldap
15. B. NIS+ 命名空间的排列因站点而异；所有站点都使用相同的结构组件：目录、表和组。这些组件被称为对象，并且可以排列成类似于 UNIX 文件系统的层次结构。
16. A. NIS+ 的四个授权类是 Owner、Group、World 和 Nobody。
17. D. 访问权限类似于文件权限。有四种类型的访问权限：read、modify、create 和 destroy。
18. C. 有三个安全级别：0、1 和 2。
19. D. 安全级别 2 是默认值。它是 NIS+ 目前提供的最高安全级别。
20. A. DNS 是互联网为传输控制协议/互联网协议（TCP/IP）网络提供的名称服务。
21. B. 每个服务器通过运行名为 in.named 的守护进程来实现 DNS。
22. B. 使用主机名作为索引查找计算机的 IP 地址的过程称为名称到地址解析或映射。DNS 的主要任务是提供名称到地址解析。
23. A. Authentication 用于识别 NIS+ 主体。NIS+ 主体可以是客户端用户或客户端工作站。每当主体（用户或系统）尝试访问 NIS+ 对象时，用户的身份和安全 RPC 密码都会得到确认和验证。Authorization 用于指定访问权限。
24. A. /etc/nsswitch.conf 文件决定如何获取特定类型的信息以及应按什么顺序查询命名服务。
25. C. Solaris 8 支持五种名称服务：/etc 文件、NIS、NIS+、DNS 和 LDAP。
26. A. DNS 是互联网使用的名称服务。
27. D. 要在主服务器上构建新映射，请键入：/usr/sbin/ypinit -m。
