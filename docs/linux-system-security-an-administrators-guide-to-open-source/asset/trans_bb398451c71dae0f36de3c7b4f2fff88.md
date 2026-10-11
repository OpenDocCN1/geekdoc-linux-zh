

# 目录

## 延伸阅读
tiger 邮件列表
sendmail 资源

## 第 14 章 Tripwire
- Tripwire 概述
- 获取和安装 Tripwire
  - Tripwire 1.2 版本
- Tripwire 配置文件
  - 扩展配置文件
- 有效地构建 Tripwire 配置文件
  - Red Hat Linux 的示例配置文件
- *tripwire* 命令
- Tripwire 初始化模式
  - 有效的 Tripwire 初始化
  - 存储数据库
- 例行的 Tripwire 运行——比较模式
  - 关于性能的说明
- Tripwire 更新模式
- 总结
- 延伸阅读
  - 在线文档
  - 网站

## 第 15 章 加密文件系统与透明加密文件系统
- 加密文件系统概述
- CFS 事件流程
- 获取和安装 CFS
- CFS 管理任务
- 使用 CFS
  - 创建和挂载 CFS 目录
  - CFS 命令和守护进程详解
  - 通过 NFS 使用 CFS
- CFS 的漏洞
- TCFS 概述
- 获取和安装 TCFS
- TCFS 客户端
- TCFS 服务器端
- 使用 TCFS
  - 配置 TCFS 以配合 PAM 使用
  - TCFS 管理任务
  - TCFS 的扩展属性
  - 设置加密目录
  - TCFS 用户组
  - TCFS 密钥管理
- TCFS 的漏洞
- CFS 与 TCFS 对比
- 安全删除文件
- CFS 和 TCFS 的替代方案
- 总结
- 延伸阅读
  - 论文
  - 邮件列表

## 第 16 章 使用 `ipchains` 进行包过滤
我们必须审查！
- 包过滤
- 为 `ipchains` 配置内核
- `ipchains` 概述
- 链的行为
- 畸形数据包
- 入站数据包分析
- 出站数据包分析
- 回环接口
- 自定义链
- 使用 `ipchains` 入门
- `ipchains` 命令
- 一些简单示例
- 数据包分片
- IP 伪装
- 添加自定义链
- 自定义链中的 ICMP 规则
- 反欺骗规则
- 规则顺序很重要！
- 保存和恢复规则
- 规则编写和日志记录技巧
- 更改规则
- `ipchains` 启动脚本
- 构建你的防火墙
  - 简单的内部网络
  - 使用 DHCP 的简单内部网络
  - `ipchains` 不仅仅是为了防火墙！
  - 还有一件事
- 辅助实用工具
- 其他示例
  - 端口转发
  - `fwconfig` GUI
  - Mason
  - 网络映射器 (`nmap`)
- 额外的防火墙软件
- 虚拟专用网络和加密隧道
- 下一代...
- 总结
- 延伸阅读
  - *iptables* 文档
  - 伪装文档
  - ISP 连接相关资源
  - 通用防火墙参考文献
  - DMZ 资源
  - ICMP 相关参考文献
- 特别致谢

## 第 17 章 日志文件管理

![](img/7933c44717ab0711177ea7153f959fc5_19_0.png)

- 通用日志文件管理
- logrotate
  - 获取和安装 logrotate
  - 配置 logrotate
  - 整合所有内容
- swatch
  - 获取 swatch
  - 安装 swatch
  - 配置和运行 swatch
- logcheck
  - 获取 logcheck
  - logcheck 的主要组件
  - 配置和安装 logcheck
  - logcheck 输出
  - logcheck 故障排除
  - 总结

## 第 18 章 实施和管理安全

![](img/7933c44717ab0711177ea7153f959fc5_19_1.png)

- 那么，我该从哪里开始？...
- 加固 Linux
  - 选择合适的工具
  - 缩小攻击面
- 如果我的系统已经处于生产环境中怎么办？...
- 内部网络
- 关键内部服务器
- 内部维护
- 防火墙和 DMZ
  - 外部维护
- 入侵恢复
- 添加新软件
- 仅通过知识

## 附录 A 保持更新

## 附录 B 未涵盖的工具

## 术语表

## 索引

# 图表

- 图 3.1 TCP/IP 模型
- 图 3.2 中继器和交换机的区别
- 图 3.3 通过加密将明文转换为密文
- 图 4.1 文件类型和权限
- 图 5.1 Linux-PAM 概述
- 图 5.2 PAM 控制的密码更改
- 图 6.1 S/Key OTP 系统
- 图 8.1 日志消息流程
- 图 10.1 TCP_Wrappers 拦截和过滤请求
- 图 11.1 RSA 基于主机的认证
- 图 11.2 Rhosts 和 RSA 认证
- 图 11.3 RSA 认证
- 图 11.4 SSH 认证流程图
- 图 11.5 使用 SSH 本地转发
- 图 12.1 Crack 目录树
- 图 12.2 Crack 中猜测过程的一般流程
- 图 12.3 规则应用于字典单词的流程
- 图 13.1 tiger 目录树
- 图 14.1 Tripwire 功能概述
- 图 15.1 CFS 事件流程
- 图 16.1 ipchains 事件流程
- 图 16.2 Linux IP 伪装
- 图 16.3 小型内部网络示例
- 图 16.4 ftp 的双重连接要求

# 示例

- 示例 3-1 在 /etc/lilo.conf 上设置安全权限和属性
- 示例 3-2 示例 /etc/lilo.conf 文件
- 示例 3-3 启动到单用户模式
- 示例 3-4 指向 /usr/sbin/lpd 的符号链接
- 示例 3-5 GPL
- 示例 4-1 截断的示例 /etc/passwd 文件
- 示例 4-2 截断的示例 /etc/shadow 文件
- 示例 4-3 /etc/login.defs 中的密码老化指令
- 示例 4-4 /etc/login.defs 中的剩余指令
- 示例 4-5 受限 Shell 程序
- 示例 4-6 /etc/fstab 文件
- 示例 4-7 更安全的 /etc/fstab
- 示例 5-1 /etc/pam.d 的内容
- 示例 5-2 PAM 配置文件条目字段
- 示例 5-3 /etc/pam.d/passwd 配置文件
- 示例 5-4 /etc/pwdb.conf 文件
- 示例 5-5 在 /etc/pam.d/passwd 中使用 mas 和 minlen
- 示例 5-6 密码更改失败
- 示例 5-7 密码更改成功
- 示例 5-8 示例 /etc/pam.d/login 文件
- 示例 5-9 在存在 /etc/nologin 的情况下尝试登录
- 示例 5-10 使用 pam_time required 的部分配置文件
- 示例 5-11 密码过期且在允许时间之外时的登录尝试 1
- 示例 5-12 使用 pam_time.so requisite 的部分配置文件
- 示例 5-13 密码过期且在允许时间之外时的登录尝试 2
- 示例 5-14 示例 /etc/security/time.conf 文件
- 示例 5-15 示例 /etc/security/limits.conf 文件
- 示例 5-16 包含 pam_listfile 条目的 csh 配置文件
- 示例 5-17 由于 pam_listfile 导致的 csh 尝试失败

