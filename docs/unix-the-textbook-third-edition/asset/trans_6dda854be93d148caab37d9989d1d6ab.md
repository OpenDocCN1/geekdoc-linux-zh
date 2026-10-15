

## 24.5.1.4 ACL 属性

ZFS 文件系统包含 ACL 属性，用于确定 ACL 继承的具体行为以及 ACL 与 chmod 命令操作之间的交互。

这些属性是：

- aclinherit：确定 ACL 继承的行为。值包括以下内容：

  - discard：对于新对象，在创建文件或目录时不继承任何 ACL 条目。文件或目录上的 ACL 等于文件或目录的权限模式。

  - noallow：对于新对象，仅继承具有拒绝访问类型的可继承 ACL 条目。

  - restricted：对于新对象，在继承 ACL 条目时移除 write_owner 和 write_acl 权限。

  - passthrough：文件根据可继承 ACE 确定模式创建。如果不存在影响模式的可继承 ACE，则模式根据应用程序请求的模式设置。

  - passthrough-x：语义与 passthrough 相同，但启用 passthrough-x 时，文件仅在文件创建模式和影响模式的可继承 ACE 中均设置执行 (x) 权限时才创建执行权限。

  ZFS aclinherit 的默认模式为 restricted。

- aclmode：在文件初始创建时修改 ACL 行为，或控制 chmod 操作期间 ACL 的修改方式。值包括以下内容：

  - discard：删除所有不代表文件模式的 ACL 条目。这是默认值。

  - mask：减少用户或组权限。权限被降低，使其不超过组权限位，除非是与文件或目录所有者具有相同 UID 的用户条目。在这种情况下，ACL 权限被降低，使其不超过所有者权限位。mask 值还保留 ACL 在模式更改期间的存在，前提是没有执行过显式的 ACL 设置操作。

  - passthrough：表示除生成必要的 ACL 条目以表示文件或目录的新模式外，不对 ACL 进行任何更改。

  ZFS aclmode 的默认模式为 discard。

## 24.5.2 在 ZFS 文件上设置 ACL

ZFS 文件上 ACL 访问的基本规则如下：

1. ZFS 按 ACL 中列出的顺序自上而下处理 ACL 条目。

2. 仅处理指定用户与访问请求者匹配的 ACL 条目。

3. 一旦授予了允许权限，就无法通过同一 ACL 权限集中后续的 ACL 拒绝条目来拒绝该权限。

4. 文件的所有者无条件地被授予 write_acl 权限，即使该权限被明确拒绝。否则，任何未指定的权限将被拒绝。在拒绝权限或缺少访问权限的情况下，特权子系统确定为文件所有者或超级用户授予的访问请求。此机制可防止文件所有者被锁定在自己的文件之外，并使超级用户能够修改文件以进行恢复。

### 24.5.2.1 设置 ACL 的命令语法

要设置或修改 ACL，请使用 chmod 命令。命令语法类似于设置文件权限位的语法，只是你在输入运算符 (+、= 或 -) 之前指定 A。

设置简单 ACL 的命令语法：

```
chmod [options] A[index]{+|=}user@ | group@ | everyone@:access-permissions/...[:inheritance-flags]:deny | allow file
```

```
chmod [options] A user@, group@, everyone@:access-permissions/...[:inheritance-flags]:deny | allow file ...
```

```
chmod [options] A[index]- file
```

设置非简单 ACL 的命令语法：

```
chmod [options] A[index]{+|=}user|group:name:access-permissions/...[:inheritance-flags]:deny | allow file
```

```
chmod [options] A user|group:name:access-permissions/...[:inheritance-flags]:deny | allow file ...
```

```
chmod [options] A[index]- file
```

chmod 命令使用以下运算符：

- A+ 添加一个 ACL 条目。

- A= 替换一个 ACL 条目。

要替换文件的整个 ACL，请在不指定索引 ID 的情况下使用此运算符。在以下示例中，file.1 的 ACL 条目将被删除并替换为 everyone@ 的单个条目。

