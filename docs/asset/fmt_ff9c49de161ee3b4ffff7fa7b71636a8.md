
```bash
#!/usr/bin/env bash
{
  1_pkgoutput="1= output2=""
  # 检查是否安装了 GNOME 桌面管理器。如果未安装该包，建议为不适用
  # 确定系统的包管理器
  if command -v dpkg-query /dev/null 2>&1; then
    1_pq="dpkg-query -W"
  elif command -v rpm /dev/null 2>&1; then
    1_pq="rpm -q"
  fi
  # 检查是否安装了 gdm
  1_pcl="gdm3" # 检查的包列表
  for lp in $1_pcl; do
    if $1_pq "$lp" >/dev/null 2>&1 && 1_pkgoutput="$lp"
系统存在包 \$lp\n 检查配置
    echo -e "$1_pkgoutput"
  done
  # 检查配置（如果适用）
  if [ -n "$1_kfile" ]; then
    echo -e "$1_kfile"
  fi
  # 查找空闲延迟以确定用户中的配置，用于剩余
  # 测试
  1_kfile="@autorun-never*" /etc/dconf/db/.*
  # 根据 dconf 数据库设置配置名称 ({PROFILE_NAME})。
  if [ -f "$1_kfile" ]; then
    1_gpname=$(awk -F/ '{split($NF-1,");print $1}' "$1_kfile")
  fi
  # 如果配置名称存在，继续
  if [ -n "$1_gpname" ]; then
    1_gpdir="/etc/dconf/db/\$1_gpname.db"
    # 检查配置文件是否存在
    if grep -P "--system-db" /etc/dconf/profile/*"; then
      1_output="$1_output - dconf 数据库文件 \"$(grep -Pl """system-db\"" /etc/dconf/profile/*\") 存在"
    else
      1_output2="$1_output2 - dconf 数据库未设置"
    fi
    # 检查 dconf 数据库是否存在
    if [ -f "/etc/dconf/db/\$1_gpname" ]; then
      1_output="$1_output - dconf 数据库 \"$1_gpname\" 存在"
    else
      1_output2="$1_output2 - dconf 数据库 \"$1_gpname\"\n不存在"
    fi
    # 检查 dconf 数据库目录是否存在
    if [ -d "$1_gpdir" ]; then
      1_output="$1_output - dconf 目录 \"$1_gpdir\" 存在"
    else
      1_output2="$1_output2 - dconf 目录 \"$1_gpdir\"\n不存在"
    fi
    # 检查 autorun-never 设置
    if grep -Pqs "^\/autorun-never\h\=true\b" "$1_kfile"; then
      1_output="$1_output - \"autorun-never\" 在此处设置为 true:"
    fi
  fi
}
}
```

```bash
"$1_kfile"
else
    1_output2="$1_output2\n - \"aurun-never\" 未被正确设置
    fi
else
    # 设置不存在。无须进一步检查
    1_output2="$1_output2\n - \"aurun-never\" 未设置
    fi
else
    1_output="$1_output - 系统上未安装 GNOME 桌面管理器包\n - 建议不适用。\n
    fi
    # 报告结果。如果 1_output2 中没有失败，则通过
    if [ -z "$1_output2" ]; then
        echo -e "\n- 审计结果:\n ** PASS **\n$1_output\n"
    else
        echo -e "\n- 审计结果:\n ** FAIL **\n - 审计失败原因:\n$1_output2\n"
        [ -n "$1_output" ] && echo -e "\n- 设置正确:\n$1_output\n"
    fi
fi
```

# 修复方案：

运行以下脚本为 `GDM` 用户将 `autorun-never` 设置为 `true`：

```bash
#!/usr/bin/env bash

{
  l_pgoutput="1" output="1" output2=""
  l_gname="local" # 设置默认 dconf 配置文件名称（默认为 local）
  # 检查是否安装了 GNOME 桌面管理器。如果包未安装

else
echo " - 在 \$$1_kfile 中创建或更新 \"autorun-never\" 条目"
  if grep -Pq '\h*autorun-never' "$1_kfile"; then
    sed -ri 's/(\S*)/autorun-never\s*=\S*/\1/3/' "$1_kfile"
  else
    if grep -Pq '\h*[^\]][/org/gnome/desktop/media-handling]\b'
    "$1_kfile" && echo "[org/gnome/desktop/media-handling]" >> "$1_kfile"
    echo '\nautorun-never=true' >> "$1_kfile"
    fi
  else
  echo -e "\n 系统上未安装 GNOME 桌面管理器包\n 建议不适用"
  fi
  # 更新 dconf 数据库
dconf update
```

`false`

# `CIS` 控制：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
| --- | --- | --- | --- | --- |
| v8 | 10.3 禁用移动介质的自动运行和自动播放 | 禁用移动介质的自动运行和自动播放执行功能。 | | ● ● |
| v7 | 8.5 配置设备不自动运行内容 | 配置设备使其不从移动介质中自动运行内容。 | | ● ● |

# `MITRE ATT&CK` 映射：

| 技术 / 子技术 | 战术 | 缓解措施 |
| --- | --- | --- |
| T1091 | | |

### 1.8.9 确保 `GDM` `autorun-never` 不被覆盖（自动化）

配置适用性：

- Level 1 - 服务器
- Level 1 - 工作站

描述：

`autorun-never` 允许 `GNOME` 桌面显示管理器通过 `GDM` 禁用自动运行。

通过使用 `dconf` 中的锁定模式，防止用户更改特定设置。

要锁定 `dconf` 键或子路径，请在 `keyfile` 目录中创建一个 `locks` 子目录。此目录下的文件包含要锁定的键或子路径列表。与 `keyfile` 一样，你可以向此目录添加任意数量的文件。

示例锁文件：

```bash
# 锁定桌面媒体处理设置
/org/gnome/desktop/media-handling/autorun-never
```

原理：

移动介质上的恶意软件在介质插入系统时可能会利用自动运行功能并执行。

审计：

运行以下脚本以验证 `autorun-never=true` 不会被覆盖：

```bash
#!/usr/bin/env bash
{
  # 检查是否安装了 GNOME 桌面管理器。如果包未安装，建议不适用\n
  # 确定系统的包管理器
  1_pkgoutput=""
  if command -v dpkg-query > /dev/null 2>&1; then
    1_pkg=$(dpkg-query -W)
  elif command -v rpm > /dev/null 2>&1; then
    1_pkg=$(rpm -q)
  fi
  # 检查是否安装了 GDM
  1_lcl="gdm" # 检查的包列表
  for 1_ln in $1_lcl; do
    [ "$1_pkg" = "$1_ln" ] > /dev/null 2>&1 && 1_pkgoutput="$1_pkg" || \
    Package:"$1_ln 存在于系统 - 正在检查配置"
  done
  # 检查配置（如果适用）
  if [ -n "$1_pkgoutput" ]; then
    1_output="$1_pkgoutput"
  fi
  # 查找空延迟以确定使用的配置，后续测试需要
  1_kfd="/etc/dconf/db/ | grep '^\h*autorun-never*' \
    /etc/dconf/db/ | awk -F'/' '{split($NF-1,a, ","); print a[1]}.d" # 设置
    要锁定键的目录"
  if [ -z "$1_kfd" ]; then if 键目录不存在，则可以锁定选项
  fi
  if grep -P '^\h* /org/gnome/desktop/media-handling/autorun-never*' "$1_kfd"; then
    1_output="$1_output \"autorun-never\" 已在 \$(grep
      -P '^\h*/org/gnome/desktop/media-handling/autorun-never*' "$1_kfd") "$1_kfd")"
  else
    1_output="$1_output2\n \"autorun-never\" 未锁定"
  fi
  else
    1_output="$1_output2\n \"autorun-never\" 未设置，因此无法锁定"
  fi
  else
    1_output="$1_output\n - 系统上未安装 GNOME 桌面管理器包 - 建议不适用"
  fi
  # 报告结果。如果 1_output2 中没有失败，则通过
  if [ -z "$1_output2" ]; then
    echo -e "\n- 审计结果:\n ** PASS **\n$1_output\n"
  else
    echo -e "\n- 审计结果:\n ** FAIL **\n - 审计失败原因:\n$1_output2\n"
    [ -n "$1_output" ] && echo -e "\n- 设置正确:\n$1_output\n"
  fi
fi
```

# `CIS` 控制：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 4.8 卸载或禁用企业资产和软件上不需要的服务 | 卸载或禁用企业资产和软件上不需要的服务，例如未使用的文件共享服务、Web应用程序模块或服务功能。 | | ● | ● |
| v7 | 9.2 确保仅运行已批准的端口、协议和服务 | 确保每个系统上仅运行了经过验证的业务需求的网络端口、协议和服务。 | | ● | ● |

# `MITRE ATT&CK` 映射：

| 技巧 / 子技术 | 战术 | 缓解措施 |
|---|---|---|
| T1040, T1040.000, T1056, T1056.001, T1557, T1557.000 | TA0002 | M1050 |

## 1.9 确保已安装更新、补丁和额外的安全软件（手动）

配置适用性：

- 级别1 - 服务器
- 级别1 - 工作站

描述：

包含的软件会定期发布补丁，可能是由于安全漏洞，也为了包含额外功能。

原理：

较新的补丁可能包含安全增强功能，这些功能无法通过最新的完整更新直接获得。因此，建议使用最新的软件补丁以利用最新功能。与软件安装一样，组织需要确定特定的更新是否符合其需求，并针对所选的更新版本验证任何额外软件的兼容性和可支持性。

审计：

验证没有待安装的更新或补丁：

```
# apt -s upgrade
```

修复：

运行以下命令，根据本地站点策略关于应用更新和补丁的指导更新所有软件包：

```
# apt upgrade
```

或者

```
# apt dist-upgrade
```

# 附加信息：

站点策略可能强制要求在将可用更新安装到生产系统之前进行测试期。

- `upgrade` 用于从 `/etc/apt/sources.list` 中列出的源安装系统中当前安装的所有软件包的最新版本。当前已安装且有新版本的软件包将进行检索并升级；在任何情况下，都不会删除当前安装的软件包，也不会安装尚未检索和安装的软件包。对于当前安装的无法在更改另一个软件包安装状态的情况下升级的新版本软件包，将保持当前版本。必须先执行更新，以便 `apt` 知道有新版本的软件包可用。

- `dist-upgrade` 除了执行 `upgrade` 功能外，还会智能地处理新版本软件包的依赖关系；`apt` 拥有一“智能”冲突解决系统，必要时它将尝试以不重要的软件包为代价升级最重要的软件包。因此，`dist-upgrade` 命令可能会删除某些软件包。`/etc/apt/sources.list` 文件包含所需软件包文件的位置列表。另见 `apt_preferences(5)` 关于覆盖单个软件包通用设置的机制。

# `CIS` 控制：

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 7.3 执行自动化操作系统补丁管理 | 每月或更频繁地通过自动化补丁管理对企业资产进行操作系统更新。 | | | | |
| | 3.4 部署自动化操作系统补丁管理工具 | 部署自动化软件更新工具，以确保操作系统运行软件供应商提供的最新安全更新。 | | | | |
| | 3.5 部署自动化软件补丁管理工具 | 部署自动化软件更新工具，以确保所有系统上的第三方软件运行软件供应商提供的最新安全更新。 | | | | |

## 2 服务

应用系统更新和补丁有助于修复已知漏洞，但保护系统免受尚未报告漏洞的最佳方法之一是禁用正常系统运行不需要的服务。这可以防止以后发现的漏洞被利用。如果服务未被启用，它就无法被利用。本文此部分的章节提供了某些可以安全禁用的服务及其情况指导，大大减少了目标系统的可能威胁。此外，还涵盖了一些应保持启用但需要安全配置的服务以及不安全的服务客户端。

注意：这不应视为不安全服务的完整列表。您可能希望根据自己的环境对此处列出的进行补充。

### 2.1 配置时间同步

建议缺乏直接访问物理宿主机时钟的物理系统和虚拟机配置使用 `systemd-timesyncd`、`chrony` 或 `ntp` 等服务来同步时间。

注意：

- 如果可以访问物理宿主机时钟并根据站点策略进行了配置，可以跳过此节
- `系统上应只使用一种时间同步方法`
- 仅遵循与使用的时间同步方法相关的章节，跳过所有其他时间同步建议
- 如果可以访问物理宿主机时钟并根据站点策略进行了配置：
    - 应当停止并掩码 `systemd-timesyncd`
    - 从系统中移除 `chrony`
    - 从系统中移除 `ntp`

# 2.1.1 确保使用时间同步

建议缺乏直接访问物理宿主机时钟的物理系统和虚拟机配置使用 `systemd-timesyncd`、`chrony` 或 `ntp` 等服务来同步时间。

# 2.1.1 确保仅使用单一同步守护进程（自动化）

配置适用性：

- 级别1 - 服务器
- 级别1 - 工作站

描述：

所有系统之间应该同步系统时间。

注意：

- 如果可以访问物理宿主机时钟并根据站点策略进行了配置，可以跳过此节
- `系统上应只使用一种时间同步方法`
- 仅遵循与使用的时间同步方法相关的章节，跳过所有其他时间同步建议
- 如果可以访问物理宿主机时钟并根据站点策略进行了配置：
    - 应当停止并掩码 `systemd-timesyncd`
    - 从系统中移除 `chrony`
    - 从系统中移除 `ntp`

原理：

配置多个同步方法可能会意外或不可靠的结果。时间同步对于支持安全机制至关重要，并确保日志文件记录一致。

审计：

运行脚本验证是否存在单一同步守护进程：
