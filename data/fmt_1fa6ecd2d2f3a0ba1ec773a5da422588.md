
### `DUMPSHMEM` 和 `DUMPCORE` 表示是，`0` 表示否。

| 参数 |  |
| :--- | :--- |
| `DUMPDIR` `/tmp` | 在此目录保留诊断信息 |
| `DUMPSHMEM` `1` | 导出共享内存 |
| `DUMPCORE` `0` | 使用 `gcore` 导出核心映像 |
| `DUMPCORE` `0` | 导出核心映像（警告：这将终止 Dynamic Server） |

- `DUMPCNT` 单用户会话的内存或 `gcore` 转储
- `FILLFACTOR` `90` 构建索引的填充因子

```
## Dynamic Server 用于确定当前时间的方法
USETIME 0 # 0: 内部时间（快），1: 从 OS 获取（慢）
```

```
## 并行数据库查询 (pdq)
MAX_PDPRIORITY 100 # 最大允许的 pdq优先级
DS_MAX_QUERIES # 最大决策支持查询数
DS_TOTAL_MEMORY # 决策支持内存（Kbytes）
DS_MAX_SCANS 1048576 # 最大决策支持扫描数
DATASKIP # 要跳过的数据库列表
```

```
## OPTCOMPIND
# 0 => 在可能的情况下，嵌套连接优于排序合并连接和哈希连接。
# 1 => 如果事务隔离模式不是“可重复读”，优化器的行为如译文 (2)。
### 否则，行为如上文 (0)。
# 2 => 无论事务隔离模式如何都使用成本。嵌套连接并不一定优先。
# 优化器完全根据成本做出决策。
OPTCOMPIND 2 # 提示优化器
```

```
CNDBSPEDOWN 2 # Dbspace 关闭选项：0 = 继续，1 = 终止，2 = 等待
LEU_PRESERVE 0 # 为日志备份保留最后的日志
OPCHEMAX 0 # 最大光学缓存大小（Kbytes）
```

```
## HETERO_COMMIT（网关在分布式事务中的参与）
### 1 => 启用异构提交
### 0（或任何其他值） => 禁用异构提交
HETERO_COMMIT 0
```

```
## 优化目标：-1 = ALL_ROWS（默认），0 = FIRST_ROWS
OPT_GOAL -1
```

```
## 优化器 DIRECTIVES （1/默认）或关闭（0）
DIRECTIVES 1
```

```
# 可重启还原的状态
RESTARTABLE_RESTORE OFF
```

## 第4 章 • 在 Linux 上安装 Informix
