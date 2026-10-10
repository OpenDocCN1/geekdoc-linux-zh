
# 示例

提取修订版本 R1 和 R2 之间的提交，并使用 `git am` 将它们应用于当前分支以进行摘取（cherry-pick）：

```
$ git format-patch -k --stdout R1..R2 | git am -3 -k
```

提取所有存在于当前分支但不存在于源分支（origin）中的提交：

```
$ git format-patch origin
```

每个提交会在当前目录中创建一个单独的文件。

提取自项目初始化以来直到 origin 的所有提交：

```
$ git format-patch --root origin
```

与上一条命令相同：

```
$ git format-patch -M -B origin
```

此外，它还会智能地检测并处理重命名和完全重写，以生成重命名补丁。重命名补丁可以减少文本输出量，通常也更易于审查。请注意，非 Git 的“patch”程序无法理解重命名补丁，因此仅当您知道接收者使用 Git 应用补丁时才使用它。

从当前分支提取最顶层的三个提交，并将其格式化为可邮件发送的补丁：

```
$ git format-patch -3
```

## 参见

git-format-patch(1), git-am(1)

# GIT-FSCK-OBJECTS

## 名称

git-fsck-objects - 验证数据库中对象的连通性和有效性

## 用法

`git fsck-objects` ...

## 描述

这是 `git-fsck(1)` 的同义词。请参阅该命令的文档。

# GIT-FSCK

## 名称

git-fsck - 验证数据库中对象的连通性和有效性

## 用法

`git fsck` [--tags] [--root] [--unreachable] [--cache] [--no-reflogs] [--[no-]full] [--strict] [--verbose] [--lost-found] [--[no-]dangling] [--[no-]progress] [<object>...]

## 描述

验证数据库中对象的连通性和有效性。

## 选项

- **<object>**
  作为不可达性追踪头部的对象。
  
  如果未给出任何对象，`git fsck` 默认使用索引文件、refs 命名空间中的所有 SHA-1 引用以及所有引用日志（除非给出了 `--no-reflogs`）作为头部。

- **--unreachable**
  打印出存在但无法从任何引用节点到达的对象。

- **--[no-]dangling**
  打印存在但从未被*直接*使用的对象（默认）。可以使用 `--no-dangling` 从输出中省略此信息。

- **--root**
  报告根节点。

- **--tags**
  报告标签。

- **--cache**
  将索引中记录的任何对象也视为不可达性追踪的头节点。

- **--no-reflogs**
  不认为仅由引用日志条目引用的提交是可到达的。此选项仅用于搜索那些曾经是某个引用中的提交，但现在不是，但仍存在于相应引用日志中的提交。

- **--full**
  不仅检查 `GIT_OBJECT_DIRECTORY`（`$GIT_DIR/objects`）中的对象，还检查在 `GIT_ALTERNATE_OBJECT_DIRECTORIES` 或 `$GIT_DIR/objects/info/alternates` 中列出的备用对象池、以及在 `$GIT_DIR/objects/pack` 和备用对象池对应的 pack 子目录中找到的打包 Git 归档中的对象。这是当前的默认行为；你可以使用 `--no-full` 关闭它。

- **--strict**
  启用更严格的检查，即捕获由旧版本 Git 创建的、设置了 g+w 位的文件模式记录。现有的存储库，包括 Linux 内核、Git 本身和稀疏存储库，都有会触发此检查的旧对象，但建议使用此标志检查新项目。

- **--verbose**
  更详细。

- **--lost-found**
  根据类型，将悬空对象写入 `.git/lost-found/commit/` 或 `.git/lost-found/other/`。如果对象是 blob，则写入文件的内容，而不是其对象名称。

- **--[no-]progress**
  当标准错误流连接到终端时，默认会在其上报告进度状态，除非指定了 `--no-progress` 或 `--verbose`。`--progress` 即使标准错误流未定向到终端也强制报告进度状态。

## 讨论

`git-fsck` 测试 SHA-1 和一般对象完整性，并对由此产生的可达性和其他所有方面进行完整追踪。它会打印出它发现的任何损坏（缺失或无效对象），如果你使用 `--unreachable` 标志，它还会打印出存在但无法从任何指定头节点（或如上所述的默认集合）到达的对象。

对于任何损坏的对象，你需要在备份或其他归档中找到它们（即，你可以直接删除它们，并对其他站点执行 `rsync`，寄希望于其他人拥有你损坏的对象）。

## 提取的诊断信息

- **expect dangling commits - potential heads - due to lack of head information**
  你未指定任何节点作为头部，因此无法区分无父提交和根节点。

- **missing sha1 directory <dir>**
  存放 sha1 对象的目录缺失。

- **unreachable <type> <object>**
  <type> 对象 <object> 实际上未在看到的任何树或提交中被直接或间接引用。这可能意味着存在未指定的其他根节点，或者树已损坏。如果你没有遗漏根节点，最好删除不可达节点，因为它们无法使用。

- **missing <type> <object>**
  <type> 对象 <object> 被引用但不在数据库中。

- **dangling <type> <object>**
  <type> 对象 <object> 存在于数据库中但从未被*直接*使用。悬空提交可能是根节点。

- **sha1 mismatch <object>**
  数据库中有一个对象的 sha1 不匹配数据库值。这表明存在严重的数据完整性问题。

## 环境变量

- **GIT_OBJECT_DIRECTORY**
  用于指定对象数据库根目录（通常是 $GIT_DIR/objects）

- **GIT_INDEX_FILE**
  用于指定索引的索引文件

- **GIT_ALTERNATE_OBJECT_DIRECTORIES**
  用于指定额外的对象数据库根目录（通常未设置）

# GIT-GC

## 名称

git-gc - 清理不必要的文件并优化本地存储库

## 用法

`git gc` [--aggressive] [-auto] [--quiet] [--prune=<date> | --no-prune] [--force]

## 描述

在当前存储库中运行许多维护任务，例如压缩文件修订版本（以减少磁盘空间并提高性能）以及删除可能由先前调用 `git add` 创建的不可达对象。

建议用户定期在每个存储库中运行此任务，以保持良好的磁盘空间利用率和良好的操作性能。

某些 `git` 命令可能会自动运行 `git gc`；有关详情，请参见下面的 `--auto` 标志。如果你知道自己在做什么，并且只想永久禁用此行为而无其他考虑，只需执行以下操作：

```
$ git config --global gc.auto 0
```

## 选项

- **--aggressive**
  通常 `git gc` 运行非常快，同时提供良好的磁盘空间利用率和性能。此选项将使 `git gc` 以更激进的方式优化存储库，代价是花费更多时间。此优化的效果是持久的，因此此选项只需偶尔使用；大约每几百个变更集一次。

- **--auto**
  带有此选项，`git gc` 检查是否需要任何维护；如果没有，它将退出不执行任何工作。一些 `git` 命令在执行可能创建许多松散对象的操作后运行 `git gc --auto`。
  
  如果存储库中有太多的松散对象或太多的 pack，则需要维护。如果松散对象数量超过配置变量 `gc.auto` 的值，则所有松散对象将使用 `git repack -d -l` 合并到单个 pack 中。将 `gc.auto` 的值设置为 0 会禁用松散对象的自动打包。
  
  如果 pack 数量超过 `gc.autoPackLimit` 的值，则使用 `git repack` 的 `-A` 选项将现有 pack（除了那些带有 `.keep` 文件标记的 pack）合并到单个 pack 中。将 `gc.autoPackLimit` 设置为 0 会禁用 pack 的自动合并。

- **--prune=<date>**
  删除早于日期 date 的松散对象（默认是 2 周前，可通过配置变量 `gc.pruneExpire` 覆盖）。`--prune=all` 无论其年龄如何都删除松散对象。`--prune` 默认开启。

- **--no-prune**
  不删除任何松散对象。

- **--quiet**
  抑制所有进度报告。

- **--force**
  强制 `git gc` 运行，即使可能还有另一个 `git gc` 实例在此存储库上运行。

