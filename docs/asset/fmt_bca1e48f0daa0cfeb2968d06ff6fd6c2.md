
# 切换每个磁盘的角色

`hastctl role primary ${disk}`

```bash
if [ $? -ne 0 ]; then
    logger -p $log -t $name "Unable to change role to primary for resource ${disk}"
    exit 1
fi
```

`logger -p $log -t $name "Role for HAST resources ${resources} switched to primary."`

# 让 HAST 脚本挂载文件系统

`service httpd start`

将此脚本复制到 `/usr/local/scripts/hast-carp-promote.sh`。

按照本节开头描述的方法测试你的脚本。一旦你确认它们可以工作，就可以编辑 `/usr/local/devd.conf` 了。

```bash
sleep 1
done
hasctl role $sname failover
```

```bash
logger -p $log -t $sname "Clear to become main storage, importing ${pools}"
```

```bash
for pool in ${pools}; do
  zpool import -f ${pool}
  if [ $? -ne 0 ]; then
    logger -p $log -t $sname "Unable to import ${pool}"
    exit 1
  fi
done
```

```bash
logger -p $log -t $sname "Pools ${pools} imported."
```

在此处启动你的服务

`service httpd start`

将此脚本拷贝到 `/usr/local/scripts/iscsi-carp-promote.sh` 并赋予其执行权限。

这里的从主到备份的脚本更为简单，只需要设置叶节点池的名称并配置用于终止使用这些池进程的命令。记住，当主机切换到备份模式时，客户端将不再访问该主机。如果有必要，你可以强制杀死（`kill`）大多数软件。

```bash
#!/bin/sh

### The names of the ZFS pools available on ISCSi
pools="data2"

#logging
log="local0.debug"
name="iscsi-carp-demote.sh"

#terminate processes here, forcibly if needed
service httpd stop

#end of user configurable stuff
for pool in ${pools}; do
  # forcibly unmount the filesystem
  zpool export -f ${pool} 2>&1
  if [ $? -ne 0 ]; then
    logger -p $log -t $sname "Unable to export ${pool}"
    exit 1
  fi
  logger -p $log -t $name "Pools ${pool} exported."
done

# if we get this far, we signal HAST that the other host can import.
hasctl role secondary failover
logger -p $log -t $name "HAST demotion triggered."
```

将此脚本拷贝到 `/usr/local/scripts/iscsi-carp-demote.sh`。如本节开头所述，请手动测试你的故障转移。一旦确定它们工作正常，就按照此处所示将它们集成到 `devd(8)` 中。

```bash
notify 30 {
  match "system" "CARP"
  match "subsystem" "[0-9]+@[0-9a-z]+"
  match "type" "MASTER"
  action "/usr/local/scripts/iscsi-carp-promote.sh"
}
```

```bash
notify 30 {
  match "system" "CARP"
  match "subsystem" "[0-9]+@[0-9a-z]+"
  match "type" "BACKUP"
  action "/usr/local/scripts/iscsi-carp-demote.sh"
}
```
