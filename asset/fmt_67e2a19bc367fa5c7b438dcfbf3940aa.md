
## `apt`

```
apt:
  preserve_sources_list: false
  primary:
    arches: [i386, amd64]
      uri: "http://archive.ubuntu.com/ubuntu"
    arches: [default]
      uri: "http://ports.ubuntu.com/ubuntu-ports"
geop: true
```

如果 `geop` 为 `true` 且使用的镜像是默认镜像，则会向 `https://geop.ubuntu.com/lookup` 发起请求，并将镜像 URI 更改为 `http://CC.archive.ubuntu.com/ubuntu`，其中 `CC` 是查找返回的国家代码（或对于 ports 来说是处理的）。如果此部分不是交互式的，请求将在 10 秒后超时。

任何指定的配置将与默认配置合并，而不是替换它。

如果你想设置镜像，请使用如下配置：

```
apt:
  primary:
    arches: [default]
      uri: YOUR_MIRROR_GOES_HERE
```

添加一个 ppa：

```
apt:
  sources:
    curtin-ppa:
      source: ppa:curtin-dev/test-archive
```

## `storage`

- `type`: mapping，见下文
- **默认**: 在单磁盘系统中使用 `lvm` 布局，多磁盘系统无默认
- **可以交互式**: yes

存储配置是复杂的，且 autoinstall 文件中对所需配置的描述也可能是复杂的。安装程序支持“布局”（layouts），这是表示常用配置的简单方法。

支持的布局：目前支持的两种布局是 `lvm` 和 `direct`。

```
storage:
  layout:
    name: lvm
```

```
storage:
  layout:
    name: direct
```

默认情况下，这些将安装到系统中最大的磁盘上，但你可以提供一个匹配规范（见下文）来指定使用哪块磁盘：

```
storage:
  layout:
    name: lvm
  match: serial*
```

```
storage:
  layout:
    name: disk
  match: ssd
```

（你只需说 `match: {}` 来匹配任意磁盘）默认使用 `lvm` 布局。为了完全灵活的基于操作的配置，安装程序允许使用 curtin 语法的超集进行存储配置，该语法在 `https://curtin.readthedocs.io/latest/topics/storage.html` 中描述。除了将操作列表放在 `config` 键下，还可以在此处交换项（swap items）。因此，一个部分看起来如下：

```
storage:
  swap:
    size: 0
  config:
    - type: format
      fst: ext4
      name: root
    - type: mount
      path: /
```

基于操作的配置在 autoinstall 文件中按顺序执行。如果存在多个匹配项，则匹配最大的磁盘：

```
type: disk
id: disk
```

对于最后一个分区，你可以指定大小为 `-1` 来表示该分区应填充剩余空间。

此处的 snap 尚未存在——autoinstall 支持带有匹配规范的创建和编辑。

## `identity`

- `type`: mapping，见下文
- **默认**: `yes`

配置系统的初始用户。这是必须存在的配置键（除非存在 `user-data` 部分，在这种情况下它是可选的）。映射包含以下键，所有值均为字符串：

### `realname`

用户的真实姓名。此字段是可选的。

### `username`

创建的用户名。

### `hostname`

系统的主机名。

### `password`

新用户的密码，需经过加密。即使配置了 SSH 访问，使用 `sudo` 也是必需的。

## `ssh`

- `type`: mapping，见下文
- **默认**: 见下文
- **可以交互式**: yes

为安装的系统配置 ssh。映射包含以下键：

### `install-server`

`type`: `boolean`  
**默认**: `false`

是否在目标系统中安装 OpenSSH 服务。

### `authorized-keys`

`type`: `string list`  
**默认**: `[]`

要安装在初始用户账户中的 SSH 公钥列表。

### `allow-pw`

`type`: `boolean`  
**默认**: 如果 `authorized_keys` 为空则为 `true`，否则为 `false`

## `snaps`

- `type`: list，安装 no 额外 snaps
- **可以交互式**: yes

要安装的 snap 列表。每个 snap 表示为一个映射，包含必需的 `name` 以及可选的 `channel`（默认为 `stable`）和 `classic`（默认为 `false`）键。例如：

## `debconf-selections`

- `type`: `string`
- **默认**: no config
- **可以交互式**: no

安装程序将更新 debconf 设置值。用户将需要熟悉包的 debconf 选项。

## `packages`

- `type`: `list`
- **默认**: no packages
- **可以交互式**: no

要安装到目标系统的软件包列表。更准确地说，是传递给 `apt-get install` 的字符串列表，因此这包含了任务选择（如 `dns-server`）和安装特定版本的软件包（如 `my-package=1-1`）。

## `late-commands`

- `type`: `command list`
- **默认**: 无命令
- **可以是交互式的**: 否

在安装成功完成并安装了任何更新后，在系统重启之前运行的 Shell 命令。这些命令将在安装程序环境中运行，并将已安装的系统挂载在 `/target`。你可以通过运行 `curtin-target --shell_command`（对于随 20.04 GA 发布的 `subiquity` 版本，你需要指定为 `curtin-target --target=/target --shell_command`）来在目标系统中运行（类似于在 d-i `preed/late_command` 中使用 `plan in-target` 的方式）。

## `error-commands`

- `type`: `command list`
- **默认**: 无命令
- **可以是交互式的**: 否

在安装失败后运行运行的 Shell 命令。这些命令将在安装程序环境中运行，并且系统（或安装管理器能够配置的部分）将挂载在 `/target`。在实时会话中，可以通过 `/var/log/installer` 查看日志。

## `reporting`

- `type`: `mapping`
- **默认**: 输出到 `tty1` 和任何配置的串口控制台的类型
- **可以是交互式的**: 否

安装程序支持向各种目的地报告进度。请注意，如果存在任何交互式部分，则此部分将被忽略；事实上，其实现与 `curtin` 使用的 90% 是相同的。

配置中 `reporting` 映射的每个键定义了一个定义，其中 `type` 子键是核心：

**rsyslog 报告器尚不存在**

- `print`: 在 `tty1` 和任何配置的串口控制台上打印进度信息。没有其他配置。
- `rsyslog`: 通过 rsyslog 报告进度。目标指定了输出的位置。
- `webhook`: 通过向 URL POST JSON 报告来报告进度。接受与 `curtin` 相同的配置。
- `none`: 不报告进度。仅用于抑制默认输出。

示例：

- 默认配置为：
- 报告到 rsyslog：
- 抑制默认输出：
- 报告到 curtin 风格的 webhook：

## `user-data`

- `type`: `mapping`
- **默认**: `{}`
- **可以是交互式的**: 否

提供 `cloud-init` `user-data`，该数据将与安装程序程序产生的 `user-data` 合并。如果你提供了此内容，则不需要提供身份部分（但要确保你可以登录到已安装的系统是你的责任！）。

## 在 amd64 上通过网络启动服务器安装程序

amd64 系统以 UEFI 或 legacy（“BIOS”）模式启动（许多系统可以配置为以一种模式启动）。具体细节取决于系统固件，但两种模式通常都支持 PXE（预启动执行环境）规范，这允许通过网络置备引导程序。

网络启动实时安装程序的过程对于两种模式都是类似的，步骤如下：

1. 将待安装机器引导至网络启动。
2. DHCP/boot 服务器告诉机器其配置以及从何处引导程序。
3. 机器的固件通过 tftp 下载引导程序并执行它。
4. 引导程序同样通过 tftp 下载配置，告诉它去哪里下载内核、ramdisk 和使用的内核命令。
5. ramdisk 查看内核命令以了解如何配置网络并下载服务器 ISO。
6. ramdisk 下载 ISO 并将其挂载为回环设备。
7. 从此时开始，安装路径与 ISO 位于本地设备时的路径相同。
