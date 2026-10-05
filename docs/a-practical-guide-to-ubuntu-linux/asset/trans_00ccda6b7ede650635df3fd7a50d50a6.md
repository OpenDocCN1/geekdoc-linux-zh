

# 目录 xvii

- 配置 OpenSSH  668
- ssh: 在远程系统上连接或执行命令 670
- scp: 在远程系统之间拷贝文件 672
- sftp: 一个安全的 FTP 客户端 674
- ~/.ssh/config 和 /etc/ssh/ssh_config 配置文件 674

- 设置 OpenSSH 服务器 (sshd) 676
- 前提条件 676
- 快速上手：启动 OpenSSH 服务器 677
- 授权密钥 (Authorized Keys): 自动登录 677
- 命令行选项 678
- /etc/ssh/sshd_config 配置文件 679

- 故障排除 680
- 隧道/端口转发 681
- 本章总结 684
- 练习 684
- 高级练习 685

# 第 19 章：FTP：跨网络传输文件 687

- FTP 简介 688
- 安全性 688
- FTP 连接 688
- FTP 客户端 689
- 更多信息 689

- 运行 ftp 和 sftp FTP 客户端 690
- 前提条件 690
- 快速上手 I：使用 ftp 下载文件 690
- 匿名登录 694
- 自动登录 694
- 二进制模式与 ASCII 传输模式 694
- ft 细节 695

- 设置 FTP 服务器 (vsftpd) 699
- 前提条件 699
- 注意事项 699
- 快速上手 II：启动 vsftpd 服务器 700
- 测试设置 700
- 配置 vsftpd 服务器 701

- 本章总结 711
- 练习 712
- 高级练习 712

# 第 20 章：exim4：设置邮件服务器、客户端及其他功能 713

- exim4 简介 714
- exim4 的替代方案 715
- 更多信息 715
- 设置邮件服务器 (exim4) 715
- 前提条件 715
- 注意事项 716
- 快速上手 I：配置 exim4 使用智能主机 (Smarthost) 716
- 快速上手 II：配置 exim4 发收接收邮件 718
- 处理 exim4 消息 720
- 邮件日志 720
- 处理消息 721
- 别名 (Aliases) 与转发 722
- 相关问题 723
- 配置 exim4 邮件服务器 724
- 使用文本编辑器配置 exim4 724
- update-exim4.conf.conf 配置文件 724
- dpkg-reconfigure: 配置 exim4 726
- SpamAssassin 727
- SpamAssassin 的工作原理 727
- 前提条件 728
- 测试 SpamAssassin 728
- 配置 SpamAssassin 730
- 额外的邮件工具 731
- 网页邮箱 (Webmail) 731
- 邮件列表 731
- 设置 IMAP 或 POP3 邮件服务器 735
- 认证中继 (Authenticated Relaying) 736
- 本章总结 738
- 练习 738
- 高级练习 739

# 第 21 章：NIS 和 LDAP 741

- NIS 简介 742
- NIS 如何工作 742
- 更多信息 744
- 运行 NIS 客户端 744
- 前提条件 745
- 注意事项 745
- 配置 NIS 客户端 746
- 测试设置 747
- yypasswd：更改 NIS 密码 748

# 目录 XXIX

- 设置 NIS 服务器 750
- 前提条件 750
- 注意事项 751
- 配置服务器 751
- 测试服务器 756
- yppasswdd：NIS 密码更新守护 757
- LDAP 758

- 更多信息 760
- 设置 LDAP 服务器 760
- 前提条件 760
- 注意事项 760
- 设置服务器 761
-向目录添加条目 764

- 用于 LDAP 的其他工具 767
- Evolution 邮件 767
- Konqueror 770

- 本章总结 770
- 练习 771
- 高级练习 771

# 第 22 章：NFS：共享文件系统 773

- NFS 简介 774
- 更多信息 776
- 运行 NFS 客户端 776
- 前提条件 776

- 快速上手 I：挂载远程目录层次 777
- mount：挂载目录层次 778
- 优化性能 780
- /etc/fstab：自动挂载目录层次 781

- 设置 NFS 服务器 782
- 前提条件 782
- 注意事项 782
- 快速上手 II：使用 shares-admin 配置 NFS 服务器 783
- 手动配置目录层次 785

- 留保存 NFS 挂载信息的地方 789
- exports：维护导出的目录列表 791
- 测试服务器 792
- automount：按需挂载目录层次 792
- 本章总结 795
- 练习 795
- 高级练习 795

# 第 23 章：SAMBA：Linux 与 Windows 文件共享 797

- Samba 简介 798
- 更多信息 799
- 注意事项 799
- Samba 用户、映射与密码 799
- 设置 Samba 服务器 800
- 前提条件 800
- 快速上手：使用 system-config-samba 配置 Samba 服务器 800
- swat：配置 Samba 服务器 804
- smb.conf：手动配置 Samba 服务器 804
- 从 Windows 访问共享 814
- 浏览共享 814
- 映射共享 814
- 从 Linux 访问共享 815
- smbtree：显示 Windows 共享 815
- smbclient：连接 Windows 共享 815
- 浏览 Windows 网络 816
- 挂载 Windows 共享 816
- 故障排除 817
- 本章总结 819
- 练习 820
- 高级练习 820

# 第 24 章：DNS/BIND：跟踪域名与地址 821

- DNS 简介 822
- 域名与子域名 824
- 区域 (Zones) 824
- 查询 825
- 响应 826
- 资源记录 (Resource Records) 827
- 反向解析 830
- DNS 如何工作 833
- 更多信息 833
- 设置 DNS 服务器 834
- 前提条件 834
- 快速上手：设置 DNS 836
- 不同类型的 DNS 850
- 缓存服务器 850
- 拆分边界 (Split Horizon) 854
- 本章总结 860
- 练习 860

# 第 25 章：ufw 和 iptables：设置防火墙 861

- ufw 简介 863
- 更多信息 864
- 注意事项 864
- 设置 ufw 866
- 前提条件 866
- 快速上手 ufw 867
- 配置防火墙 868
- 测试防火墙 874

- iptables 结构 877
- iptables 简介 880
- 更多信息 880
- 注意事项 880
- 设置 iptables 883
- 前提条件 883
- 快速上手 iptables 884
- 配置 iptables 885
- 目标 (Targets) 885
- 判定 (Criteria) 887
- 匹配 (Match) 887
- 数据包 (Packet) 887
- 命令 (Commands) 890
- 链 (Chains) 890
- 表 (Table) 891
- 连接 (Connection) 892
- NAT 893
- 过滤 (Filtering) 893
- 规则 (Rules) 895
- 本章总结 896
- 练习 896
- 高级练习 897

# 第 26 章：APACHE：设置 Web 服务器 899

- Apache 简介 900
- 更多信息 901
- 注意事项 901
- 运行 Apache 902
- 前提条件 902
- 快速上手启动 Apache 903
- 配置 Apache 905
- 指令 (Directives) 909
- 指令 I：你想修改的指令 910
- 上下文 (Contexts) 与变量 915
- 指令 II：高级指令 919
- 配置文件 932
- apache2.conf 文件 932
- 默认配置文件 934
- 高级配置 935
- 重定向 (Redirects) 935
- 内容协商 (Content Negotiation) 935
- 服务器生成的目录列表 937
- 虚拟主机 (Virtual Hosts) 937
- 故障排除 940
- 模块 (Modules) 941
- mod_cgi 和 CGI 脚本 942
- mod_ssl 943
- 认证模块与 .htaccess 945
- 脚本模块 946
- 多进程模块 (MPMs) 947
- webalizer：分析 Web 流量 948
- RTG：监控流量负载 948
- 错误代码 948
- 本章总结 949
- 练习 950
- 高级练习 950

# 第六部分 编程工具 951

# 第 27 章：编写 Bourne Shell 953

- 控制结构 954
- if...then 954
- if...then...else 958
- if...then...elif 961

- for...in 967
- for 968
- while 970
- until 974
- break 和 continue 976
- case 977
- select 983

- 文件描述符 (File Descriptors) 987
- 参数与变量 990
- 数组变量 990
- 变量的局部性 992
- 特殊参数 994
- 位置参数 996
- 扩展空和未设置变量 1001

- 内置命令 1002
- type：显示关于命令的信息 1003
- read：接受用户输入 1003
- exec：执行命令或重定向文件描述符 1006
- trap：捕获进程 1009
- kill：终止进程 1012

- getops：解析选项 1012
- 内置命令部分列表 1015
- 表达式 1016
- 算术评估 1016
- 逻辑评估（条件表达式）1017
- 字符串模式匹配 1018
- 运算符 1019

- Shell 程序 1024
- 递归 Shell 脚本 1025
- 测验 Shell 脚本 1028
- 本章总结 1034
- 练习 1036
- 高级练习 1038

# 第 28 章：Perl 脚本语言 1041

- Perl 简介 1042
- 更多信息 1042
- 帮助 1043
- perdoc 1043
- 术语 1045
- 运行 Perl 程序 1046
- 语法 1047

