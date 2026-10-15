

条目的重要性。例如，上面第一个地址匹配列表如果两个条目顺序颠倒，就不会产生预期效果，因为 1.2.3.13 会成功匹配 1.2.3.0/24，而取反的条目永远不会被遇到。

现在，来看看语句！有些简短精炼；有些几乎值得单独写一章。

## The include statement

为了拆分或更好地组织大型配置，你可以将配置的不同部分放在单独的文件中。子文件通过 include 语句被引入 named.conf：

```
include "path";
```

如果路径是相对的，则相对于 directory 选项指定的目录进行解释。include 语句的常见用途是引入不应被世界可读的加密密钥。与其关闭对整个 named.conf 文件的读取访问，一些站点将密钥保存在只有 named 可以读取的权限受限的文件中。然后这些文件被包含到 named.conf 中。

许多站点将区域语句放在单独的文件中，并使用 include 语句将其引入。这种配置有助于将相对静态的配置部分与那些可能经常变化的部分分开。

## The options statement

options 语句指定全局选项，其中一些选项以后可能被特定区域或服务器覆盖。其通用格式为

```
options {
    option;
    option;
    ...
};
```

如果 named.conf 中没有 options 语句，则使用默认值。

BIND 有很多选项——事实上太多了。9.7 版本有超过 150 个，这对系统管理员来说很多。遗憾的是，只要 BIND 团队考虑删除一些不好的想法或不再必要的选项，就会遭到使用并需要这些晦涩选项的站点的反对。我们在这里不涵盖 BIND 选项的全部范围；我们有偏见地进行了覆盖，只讨论我们推荐使用的选项。 [我们还向 BIND 开发人员征求了建议，关于应涵盖哪些选项，并遵循了他们的建议。]

有关选项的更完整覆盖，请参阅本章末尾列出的有关 DNS 和 BIND 的书籍之一。你也可以参考随 BIND 发货的文档。发行版 doc 目录中的 ARM 文档

描述每个选项并显示语法和默认值。文件 **doc/misc/options** 也包含选项的完整列表。

当我们梳理大约四分之一的可能选项时，我们添加了页边注释作为迷你索引条目。默认值列在每个选项旁边的方括号中。对于大多数站点，默认值完全没问题。选项的排列没有特定顺序。

### File locations

```
directory "path";        [directory where the server was started]
key-directory "path";    [same as directory entry]
```

directory 语句导致 **named** cd 到指定的目录。无论何时在 **named** 的配置文件中出现相对路径名，它们都相对于此目录解释。*path* 应为绝对路径。任何输出文件 [调试、统计等] 也写入此目录。key-directory 是存储加密密钥的位置；它不应被世界可读。

我们喜欢将所有 BIND 相关配置文件 [除 **named.conf** 和 **resolv.conf** 外] 放在 **/var** 下的子目录中 [或你存放其他程序配置文件的位置]。我们使用 **/var/named** 或 **/var/domain**。

### Name server identity

```
version "string";        [real version number of the server]
hostname "string";       [real hostname of the server]
server-id "string";      [none]
```

version 字符串标识服务器上运行的名称服务器软件的版本。hostname 字符串标识服务器本身，server-id 字符串也是如此。这些选项让你对真实值撒谎。它们各自将数据放入 CHAOS 类 TXT 记录中，好奇的旁观者可以用 **dig** 命令搜索它们。

我们不鼓励篡改这些值。例如，能够查询你的名称服务器并找出它们运行的版本非常方便，如果你想知道你的供应商是否提供当前版本，或需要验证你是否已将所有服务器升级到最新修订版。如果必须隐藏版本号，至少输入一个向你的系统管理员传达版本信息但不明显这样做的字符串。[新的 NSID 资源记录正好就是这样做的。此 TXT 类记录的数据部分是一个字符串值，你的系统管理员可以将其设置为对他们有意义但对世界其他地方没有意义。]

hostname 和 server-id 参数是最近的添加，由使用 anycast 路由复制根和 gTLD 服务器的实例所推动。

### Zone synchronization

```
notify yes | master-only | explicit | no;    [yes]
also-notify servers_ipaddrs;                 [empty]
allow-notify address-match-list;             [empty]
```

notify 和 also_notify 子句仅适用于主服务器，而 allow-notify 仅适用于从服务器。

