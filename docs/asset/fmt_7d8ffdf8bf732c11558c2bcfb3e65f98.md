
# CIS Controls:

| 控制版本 | 控制项 | IG 1 | IG 2 | IG 3 |
|---|---|---|---|---|
| v8 | 10.3 禁用移除式介质的自动运行和播放: 禁用移除式介质的自动运行和自动执行功能。 | | ● | ● |
| v7 | 8.5 配置设备不自动运行内容: 配置设备不自动运行移除式介质的内容。 | | ● | ● |

### 1.8.7 确保 GDM 禁用自动挂载移除式介质未被覆盖（自动化）

**配置适用性：**

*   Level 1 - 服务器
*   Level 2 - 工作站

**描述：**

默认情况下，GNOME 会为了方便用户在插入移除式介质时自动挂载。

通过使用 `dconf` 中的锁定模式，你可以防止用户更改特定设置。

要锁定 `dconf` 键或子路径，请在 `keyfile` 目录中创建一个 `locks` 子目录。该目录下的文件包含键或子路径列表。与 `keyfile` 一样，你可以向此目录中添加任意数量的文件。

示例锁定文件：

```
# 锁定桌面屏保护设置
/org/gnome/desktop/media-handling/automount
/org/gnome/desktop/media-handling/automount-open
```

**原理：**

如果启用自动挂载，任何具有物理访问权限的人都可以连接 USB 驱动器或光盘，即使他们没有挂载自身的权限，其内容也会在系统中可用。

**影响：**

工作站用户使用便携硬盘非常常见。

**审计：**

运行以下脚本以验证禁用自动挂载已锁定：

```bash
#!/usr/bin/env bash
{
  # 检查是否安装了 GNOME 桌面管理器。如果未安装该包，建议为不适用
  # 确定系统的包管理器
  1_pkgoutput=""
  if command -v dpkg-query > /dev/null 2>&1; then
    1_pq="dpkg-query -W"
  elif command -v rpm > /dev/null 2>&1; then
    1_pq="rpm -q"
  fi
  # 检查是否安装了 gdm
  1_pcl="gdm3" # 检查的包列表
  for 1_pn in $1_pcl; do
    1_output=$($1_pq "$1_pn" > /dev/null 2>&1)
    echo "系统存在包:\$1_pn - 正在检查配置"
    # 检查配置（如果适用）
    if [ -n "$1_pkgoutput" ]; then
      1_output="$1_output $1_pkgoutput"
    fi
    # 查找空闲延迟以确定用户中的配置，用于剩余
    # 测试
    1_kfd="/etc/dconf/db/$(grep -Prl '\h\*autouncount\b' /etc/dconf/db/.* | awk -F'/' '{print split($NF-1,a,".");print [1]}")" # 设置 key file 目录
    要锁定的
    1_kfd="/etc/dconf/db/$(grep -Prl '\h\*autouncount\b' /etc/dconf/db/.* | awk -F'/' '{print split($NF-1,a,".");print [1]}")" # 设置 key file 目录
    要锁定的
    if [ -d "$1_kfd" ]; then # 如果目录不存在，
    无法锁定
    if grep -Piq '\h\*/org/gnome/desktop/media-handling\*autouncount\b' "$1_kfd"; then
      1_output="$1_output - "autouncount" 在 "\$1_kfd" 中锁定"
    else
      1_output2="$1_output - "autouncount" 未锁定"
    fi
    1_output2="$1_output - "autouncount" 未设置，可以锁定
    if [ -d "$1_kfd" ]; then # 如果目录不存在，
    选项无法锁定选项
    if grep -Piq '\h\*/org/gnome/desktop/media-handling\*autoun-open\b' "$1_kfd"; then
      1_output="$1_output - "autoun-open" 在 \$(grep -Pril '\h\*/org/gnome/desktop/media-handling/automount-open\b' "$1_kfd")" 中锁定"
    else
      1_output2="$1_output - "autoun-open" 未锁定"
    fi
    1_output2="$1_output - "autoun-open" 未设置，可以
    fi
  fi
  1_output="$1_output 系统上未安装 GNOME 桌面管理器 - 建议不适用"
fi
# 报告结果。如果 $1_output2 中没有失败，则通过
[ -n "$1_pkgoutput" ] && echo -e "\n$1_pkgoutput"
if [ -z "$1_output2" ]; then
  echo -e "\n- 审计结果：\n  ** 通过 **\n$1_output"
else
  echo -e "\n- 审计结果：\n  ** 失败 **\n - 失败原因:\n$1_output2"
  [ -n "$1_output" ] && echo -e "\n- 设置正确:\n$1_output"
fi
```

**修复：**

运行以下脚本锁定所有 GNOME 用户的介质自动挂载禁用：

```bash
#!/usr/bin/env bash
{
  # 检查是否安装了 GNOME 桌面管理器。如果未安装该包，建议为不适用
  # 确定系统的包管理器
  1_pkgout=""
  if command -v dpkg-query > /dev/null 2>&1; then
    1_pq="dpkg-query -w"
  elif command -v rpm > /dev/null 2>&1; then
    1_pq="rpm -q"
  fi
  # 检查是否安装了 gdm
  1_pcl="gdm" # 检查的包列表
  for ln in $1_pcl; do
    if $1_pq "$ln" >/dev/null 2>&1 || 1_pkgout="y" && echo -e "\n系统存在包 \$ln - 正在修复配置\n"
    # 检查配置（如果适用）
    if [ -n "$1_pkgout" ]; then
    # 查找自动挂载以确定配置，用于剩余
    # 测试
    1_kfd="/etc/dconf/db/$(grep -Prl '\h*autouncount\b' /etc/dconf/db/.* | awk -F'/' '{print split($NF-1,a,".");print [1]}")" # 设置 key file 目录
    要锁定的
    1_kfd="/etc/dconf/db/$(grep -Prl '\h*autouncount\b' /etc/dconf/db/.* | awk -F'/' '{print split($NF-1,a,".");print [1]}")" # 设置 key file 目录
    要锁定的
    if [ -d "$1_kfd" ]; then # 如果目录不存在，
    无法锁定
    if grep -Piq '\h\*/org/gnome/desktop/media-handling*autouncount\b' "$1_kfd"; then
      echo -e "automount 在 \$(grep -Pril '\h\*/org/gnome/desktop/media-handling/automount\b' "$1_kfd")" 中锁定"
    else
      echo -e " 创建锁定到 automount"
      [ ! -d "$1_kfd_locks" ] && echo "创建目录 $1_kfd_locks"
      mkdir "$1_kfd_locks"
      echo -e "\n# 锁定介质处理自动挂载设置"
      echo "/org/gnome/desktop/media-handling/automount/"
      >> "$1_kfd_locks/00-media-automount"
    fi
    else
    echo -e "automount 未设置，无法锁定\n请遵循“禁用 GDM 介质自动挂载”并再次尝试"
    if [ -d "$1_kfd" ]; then # 如果目录不存在，
    无法锁定
    if grep -Piq '\h\*/org/gnome/desktop/media-handling*autoun-open\b' "$1_kfd"; then
      echo "automount-open" 在 \$(grep -Pril '\h\*/org/gnome/desktop/media-handling/automount-open\b' "$1_kfd")" 中锁定
    else
      echo " 创建条目锁定 \"automount-open\""
      { ! -d "$1_kfd/locks" && echo "创建目录 $1_kfd/locks"
      mkdir "$1_kfd/locks"
      {
        echo -e '\n锁定桌面介质处理自动挂载-open
        echo '/org/gnome/desktop/media-handling/automount-open'
      } >> "$1_kfd/00-media-automount"
    else
      echo -e " \"automount-open\" 未设置，无法锁定\n- 请遵循“禁用 GDM 介质自动挂载”并再次尝试"
    fi
    # 更新 dconf 数据库
    else
    echo -e " - 系统上未安装 GNOME 桌面包\n - 建议不适用"
  fi
```

**参考：**

*   [https://help.gnome.org/admin/system-admin/stable/dconf-lockdown.html](https://help.gnome.org/admin/system-admin/stable/dconf-lockdown.html)

### 1.8.8 确保启用 GDM autorun-never（自动化）

**配置适用性：**

*   Level 1 - 服务器
*   Level 1 - 工作站

**描述：**

`autorun-never` 设置允许 GNOME 显示管理器通过 GDM 禁用自动运行。

**原理：**

移除式介质上的恶意软件在介质插入系统时可能会利用自动运行功能并执行。

**审计：**

运行以下脚本以验证 GDM 的 `autorun-never` 已设置为 `true`：

```bash
#!/usr/bin/env bash
{
  1_pkgoutput=""
  1output=""
  profile="local" # 设置 dconf profile (local)
  # 检查是否安装了 GNOME 桌面管理器。如果未安装，建议不适用
  # 确定系统的包管理器
  if command -v dpkg-query > /dev/null 2>&1; then
    1_pkg="dpkg-query"
  elif command -v rpm > /dev/null 2>&1; then
    1_pkg=""
  # 检查是否安装了 GDM
  pcl="gdm3" # 需要检查的包列表
  for 1_in in $1_pcl; do
    $1_pkg "$1_in" > /dev/null 2>&1 && 1_pkgoutput="$1_pkgoutput\n 系统上存在包:$1_in"
  done
  echo -e "$1_pkgoutput"
  # 检查配置（如果适用）
  if [ -n "$1_pkgoutput" ]; then
    echo -e "$1output"
    # 查找已设置并设置变量
    1_keyfile=$(grep -P "|'/home/account\b/etc/dconf/db.*")
    1_key2=$(grep -P "|'/home/account-open\b/etc/dconf/db.*")
    # 根据 dconf 目录设置 profile 名称 (PROFILE_NAME)
    if [ -f "$1_keyfile" ]; then
      1_gpname=$(awk -F'/' '{split($NF-1,",");print $a[1]}') <<< "$1_keyfile"
      echo -e "更新 dconf profile 名称为 \$1_gpname"
    elif [ -f "$1_key2" ]; then
      1_gpname=$(awk -F'/' '{split($NF-1,",");print $a[1]}') <<< "$1_key2"
      echo -e "更新 dconf profile 名称为 \$1_gpname"
    fi
    # 检查一致性（需要时清理）
    if [ -f "$1_keyfile" ] && [ "$(awk -F'/' '{split($NF-1,",");print $a[1]}' <<< "$1_keyfile")" != "$1_gpname" ]; then
      sed -i "/s/^$account\s=.**/" "$1_keyfile"
      1_keyfile=/etc/dconf/db/$1_gpname.d00-media-automount
    fi
    if [ -f "$1_key2" ] && [ "$(awk -F'/' '{split($NF-1,",");print $a[1]}' <<< "$1_key2")" != "$1_gpname" ]; then
      sed -i "/s/^$account-open\s=.**/" "$1_key2"
    fi
    if [ -n "$1_keyfile" ] && [ -f "/etc/dconf/db/$1_gpname.d00-media-automount" ]; then
      # 检查 profile 文件是否存在
      if grep -Pq "\system-db:$1_gpname\b" /etc/dconf/profile/*; then
        echo -e "\n dconf 数据库 profile 存在: \$(grep -Pl "\system-db:$1_gpname\" /etc/dconf/profile/*)"
      else
        echo -e "\n 未设置 dconf 数据库 profile"
        1_outputfile=/etc/dconf/profile/user
# 检查 automount 设置
if grep -P '^auttomount-behavior=false' "$1_kfile"; then
    1_output="$1_output\n - \"automount\" 已设置为 false"
else
    1_output="$1_output2\n - 未设置 \"automount\""
fi
# 检查 automount-open 设置
if grep -P '^auttomount-open=false' "$1_k2"; then
    1_output="$1_output\n - \"automount-open\" 已设置为 false"
else
    1_output="$1_output2\n - 未设置 \"automount-open\""
fi
```
