
# /sys/devices/system/node

The `mem.sh` script inspects the memory available to each CPU node. In a true NUMA system, if all of a node's CPUs were offline, the memory associated with that node would not be available. In the way that Linux works on `x86_64` architecture, the memory is still available, although the CPU is marked as being offline for processing duties.

```bash
$ cat mem.sh
#!/bin/bash

kb=`head -1 /proc/meminfo | awk '{ print $2 }'`
mb=`echo 'scale=2; $kb / 1024' | bc`
gb=`echo 'scale=2; $mb / 1024' | bc`
echo "Server has $gb Gb ($kb KB)"

cd /sys/devices/system/node
grep MemTotal node meminfo | while read name node memtotal kb
do
mb=`echo 'scale=2; $kb / 1024' | bc`
gb=`echo 'scale=2; $mb / 1024' | bc`
echo "Node $node has $gb Gb.
* grep -w 1 /sys/devices/system/node/node/cpu[0-9]* | wc -1 CPUs online"
done
```

`mem.sh` 脚本检查了每个 CPU 节点可用的内存。在真正的 NUMA 系统中，如果一个节点的所有 CPU 都处于离线状态，与该节点关联内存将无法像 Linux 在 `x86_64` 架构上工作那样可用——内存仍然可用，尽管 CPU 被标记为离线以进行处理任务。

```bash
$ cat mem.sh
#!/bin/bash

kb=`head -1 /proc/meminfo | awk '{ print $2 }'`
mb=`echo 'scale=2; $kb / 1024' | bc`
gb=`echo 'scale=2; $mb / 1024' | bc`
echo "Server has $gb Gb ($kb KB)"

cd /sys/devices/system/node
grep MemTotal node meminfo | while read name node memtotal kb
do
mb=`echo 'scale=2; $kb / 1024' | bc`
gb=`echo 'scale=2; $mb / 1024' | bc`
echo "Node $node has $gb Gb.
* grep -w 1 /sys/devices/system/node/node/cpu[0-9]* | wc -1 CPUs online"
done
```
