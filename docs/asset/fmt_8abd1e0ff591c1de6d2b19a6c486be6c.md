
```bash
#!/bin/bash
#
# RPM 研究：查询 RPM 数据库
echo 'Enter the name of an RPM or file'
read RPM
echo 'select a task from the menu'
select TASK in 'Check from which RPM this file comes' 'Check if this RPM is installed' 'Install this RPM' 'Remove this RPM'
case $REPLY in
    1) TASK="-rpm $RPM";
    2) TASK="-rpm -qa | grep $RPM";
```

## 使用 select 命令

- 3) TASK="rpm -ivh $RPM";;

4) TASK="rpm -e $RPM";;

```
if [ -n "$TASK" ]
then
    echo TASK
else
    echo invalid
done
```

# 第 19 章：理解启动过程

- 1. 答案如下：

```bash
#!/bin/bash
#
# 监控进程 httpd
#
COUNTER=0
while ps aux | grep httpd | grep -v grep > /dev/null

    COUNTER=$((COUNTER+1))
    sleep 1
    echo COUNTER IS $COUNTER
done

logger HTTPMONITOR: httpd stopped at `date'
/etc/init.d/apache2 start
mail -s Apache server just stopped root < .
```

- 2. 答案如下：

```bash
#!/bin/bash
#
# RPM 研究：查询 RPM 数据库
echo 'Enter the name of an RPM or file'
read RPM
echo 'select a task from the menu'
select TASK in 'Check from which RPM this file comes' 'Check if this RPM is installed' 'Install this RPM' 'Remove this RPM'
case $REPLY in
    1) TASK="-rpm $RPM";
    2) TASK="-rpm -qa | grep $RPM";
    3) TASK="rpm -ivh $RPM";;
4) TASK="rpm -e $RPM";;
esac
```

if [ -n "$TASK" ]

then

    echo TASK

else

    echo invalid

fi

```

# 第 20 章：引入高可用性

- 1. 答案如下：
```bash

#!/bin/bash

#

# 监控进程 httpd

#

COUNTER=0

while ps aux | grep httpd | grep -v grep > /dev/null

    COUNTER=$((COUNTER+1))

    sleep 1

    echo COUNTER IS $COUNTER

done

logger HTTPMONITOR: httpd stopped at `date'

/etc/init.d/apache2 start

mail -s Apache server just stopped root < .

```

- 2. 答案如下：
```bash

#!/bin/bash

#

# RPM 研究：查询 RPM 数据库

echo 'Enter the name of an RPM or file'

read RPM

echo 'select a task from the menu'

select TASK in 'Check from which RPM this file comes' 'Check if this RPM is installed' 'Install this RPM' 'Remove this RPM'

case $REPLY in

    1) TASK="-rpm $RPM";

    2) TASK="-rpm -qa | grep $RPM";

    3) TASK="rpm -ivh $RPM";;

    4) TASK="rpm -e $RPM";;

esac

```
if [ -n "$TASK" ]
then
    echo TASK
else
    echo invalid
fi
```

# 第 21 章：设置服务器

确保执行了以下任务：

- 1. 创建目录后，使用 `semanage fcontext -a httpd_sys_content_t "web/.*"` 然后执行 `restorecon -r /web`。这确保了 SELinux 允许访问非默认文档根目录。

- 2. 使用编辑器在相应的文档目录下创建一个 `index.html` 文件。

- 3. 在 `/etc/httpd/conf.d` 中，为每个虚拟主机创建一个配置文件。确保在这些文件中至少使用了以下指令：

```
<VirtualHost *:80>
  ServerAdmin webmaster@server1.example.com
  DocumentRoot /www/docs/server1.example.com
  ServerName server1.example.com
  ErrorLog logs/server1.example.com-error_log
  CustomLog logs/server1.example.com-access_log common
</VirtualHost>
```

# 术语表609

`cgroups` 在性能优化中，`cgroup` 是一个预定义的资源组。通过使用 `cgroups`，可以对系统资源进行分组并仅为特定进程保留。可以配置 `cgroups`，使得只有允许的进程才能访问其资源。

`chain`（链）在 Netfilter 防火墙中，链是一系列过滤规则。链中的规则始终按顺序进行处理，直到找到匹配项为止。

通用 Internet 文件系统 (`CIFS`) 通用 Internet 文件系统是一种是一种基于服务器消息块 (`SMB`) 协议规范的文件共享解决方案。该规范最初由 IBM 为其 OS/2 操作系统开发，后由微软适配，微软于 1995 年发布了该规范。在 Linux 上，`CIFS` 在 Samba 服务器中实现，通常用于企业环境的文件共享。`CIFS` 也是 NAS（网络存储设备）应用中的常用解决方案。

`command substitution`（命令替换）这是脚本中的一种技术，用于在脚本中使用命令的结果。通过使用命令替换，可以创建一个灵活的 shell 脚本来执行特定命令的结果，而该结果可能根据执行时的条件而有所不同。

完全公平队列 (`CFQ`) 在内核调度器优化中，`CFQ` 是一种让读请求和写请求具有相同优先级的方法。`CFQ` 是默认调度器，它以相同的优先级对待读和写请求。由于这种对等对待，对于专注于读请求或写请求的服务器来说，这可能不是实现最佳性能的最佳方法。

`Conga` 在 Red Hat 高可用性（Red High Availability）插件中，`Conga` 是基于 Web 的管理平台的名称，由 `ricci` 代理和 `luci` 管理界面组成。

`context`（上下文）在 LDAP 中，上下文是 LDAP 目录中的一个位置。LDAP 客户端通常会配置一个默认上下文，这是客户端在 LDAP 目录中查找对象的默认位置。

`controllers`（控制器）在 `cgroups` 中，可以控制不同类型的系统资源。`cgroups` 使用控制器来定义提供的资源访问类型。例如，为内存、CPU 周期和 I/O 提供不同的控制器。

`copyleft license`（左岸许可）左岸许可是版权许可的开源替代方案。在一种左岸许可中，权利由一个组织主张；而在另一种左岸许可中，权利不被主张，而是留给普通公众。

`Corosync` 这是 Red Hat 高可用性插件的一部分，负责集群的底层工作。`Corosync` 使用 `Totem` 协议来验证集群中的其他节点是否可用。

`cron daemon`（cron 守护进程）`Cron` 是一个用于调度任务的守护进程（进程）。`cron` 守护进程根据 `/etc/crontab` 文件定义的设置执行任务。

![](img/3a7e027360b64bc83d5cf9a2db902251_638_0.png)

# D

`daemons`（守护进程）守护进程是 Linux 服务进程。要启动它们，你通常会使用 `service` 命令。

`deadline scheduler`（截止调度器）这是一种调度器设置，在写入磁盘之前尽可能等待。通过这种方式，它确保了写入操作以最高效率执行。建议在优化多于读的服务器时使用截止调度器。
