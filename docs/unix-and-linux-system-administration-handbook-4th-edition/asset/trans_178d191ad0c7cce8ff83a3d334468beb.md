

默认情况下，大多数系统都附带了适用于独立机器的 nsswitch.conf 文件。所有条目都指向平面文件，除了主机查找，先查询平面文件然后查询 DNS。少数系统对 passwd 和 group 默认使用 compat 模式，这可能值得更改。如果你确实使用 NIS，就明确将其写入 nsswitch.conf 文件。

### nscd：缓存查找结果

在某些 Linux 发行版中，另一个参与系统文件处理的组件是 nscd，即名称服务缓存守护进程，其名称有些误导。

nscd 与 C 库协同工作，缓存 getpwent 等库调用的结果。nscd 只是这些库例程的包装器；它对实际查询的数据源一无所知。理论上 nscd 应该能提升查找性能，但从用户角度来看，任何提升都几乎无法察觉。

我们说“名称服务缓存守护进程”具有误导性，因为“名称服务”一词通常指的是 DNS，即在主机名和 Internet 地址之间进行映射的分布式数据库系统。nscd 确实会缓存 DNS 查找结果（因为它包装了 gethostname 等），但它也会包装访问 passwd 和 group 文件及其网络数据库等价物的库例程。 （出于安全考虑，对 /etc/shadow 的查找不会被缓存。）

从概念上讲，nscd 除了加快重复查找之外，不应对系统的运行产生任何影响。实际上，它可能导致意外行为，因为它维护着查找结果的自己的副本。查找结果会在缓存中保留固定时间（在 nscd 的配置文件 /etc/nscd.conf 中设置），并且总有可能最近的更改在旧数据超时之前不会反映在 nscd 的缓存中。nscd 足够智能，能够监控本地数据源（例如 /etc/passwd）的更改，因此本地更新应在 15 秒内传播。对于通过 NIS 等检索的远程条目，你可能必须等待完整的超时时间后更改才会生效。

在我们的示例发行版中，只有 SUSE 默认运行 nscd。Red Hat 安装了 nscd，但默认在启动时不启动它；要启用 nscd 的使用，请运行 chkconfig nscd on。Ubuntu 与 nscd 兼容，但默认安装中不包含 nscd；运行 apt-get install nscd 即可下载它。

nscd 在启动时启动并持续运行。默认的 /etc/nscd.conf 对 passwd 数据指定 10 分钟超时，对 hosts 和 group 指定一小时超时，负向超时为 20 秒（即在重新尝试不成功查找之前的等待时间）。实际上，这些值很少需要更改。如果你最近做的更改似乎没有显示出来，nscd 很可能是原因。

请参阅第 17 章了解有关 DNS 的更多信息。

### 19.6 **推荐阅读**

- Carter, Gerald. *LDAP System Administration*. Sebastopol, CA: O’Reilly Media, 2003.
- Malère, Luiz Ernesto Pinheiro. *LDAP Linux HOWTO*. tldp.org
- Voglmaier, Reinhard. *The ABCs of LDAP: How to Install, Run, and Administer LDAP Services*. Boca Raton, FL: Auerbach Publications, 2004.
- *LDAP for Rocket Scientists*. zytrax.com/books/ldap

### 19.7 **练习**

- E19.1 为什么“拉取”方法更新本地机器文件比“推送”方法更安全？
- E19.2 解释 **rdist** distfile 中的以下摘录：

  ```text
  LINUX_PASSWD = ( redhatbox unbox susbox )
  passwd:
      ( /etc/passwd ) -> ( ${LINUX_PASSWD} )
      install /etc/passwd:dist;
      cmds special /etc/passwd rdist "-u/local/bin/mkpasswd";
  ```

- ★ E19.3 解释 **rdist** 与 **rsync** 之间的区别。在什么情况下使用其中一个会比另一个更好？
- ★ E19.4 你使用什么方法共享系统文件？该方法有哪些安全问题？建议一种在你站点共享系统文件的替代方法，并详细说明它解决的问题。有什么缺点吗？
- ★★★★★ E19.5 设计一个 LDAP 模式，用于存储用户信息，如登录名、密码、shell、授权机器等。构建一个工具，可交互地或从包含用户列表的文件中将新用户输入数据库。构建一个工具，可从 LDAP 数据库为实验室中的机器生成 **passwd**、**group** 和 **shadow** 文件。允许用户在每台机器上使用不同的密码（如果他们愿意）。 （并非所有用户都一定有权使用每台计算机。）你的 **adduser** 系统应能够打印现有用户登录名列表，并为新用户打印登录名/密码对。

