
**列表 27-20** 我们期望的列表 27-20 中的 `build_default_conf` 函数

## 第 27 章 使用 Dirvish 和 rsync 创建快照类型备份 889

为了压缩索引，我们使用大括号内的所有 `echo` 语句，然后使用单个输出重定向来创建 `OUTFILE`。
`build_default_conf` 函数创建的字段是一个临时文件，而不是我们需要在新 vault 中创建的 `default.conf` 文件。最后一步是创建新 vault 并新创建的 `default.conf` 复制到新创建的 vault 中。
其余代码在列表 27-21 中。

```bash
echo -e "\ncreating default.conf Dirvish Configuration File for $HN"

build_default_conf $HN "$BANK" $DAYS "$STREE" "$IGNORE_LIST"

echo -e "\ncopying file to: ${BANK/($HN)/dirvish/default.conf"

cp -f $DEFAULT_CONF ${BANK/}/($HN)/dirvish/default.conf

echo -e "\n...Press ENTER to Continue...\c"

read ANS
```

列表 27-21 用于创建新的 `default.conf` 文件

在 27-21 中，我们告知用户我们正在创建新的 `default.conf` 文件，然后调用 `build_default_conf` 函数，传递主机名、bank、过期前的天数、要备份的树以及要忽略的文件和目录列表。注意 `"$BANK"`、`"STREE"` 和 `"IGNORE_LIST"` 都包含在双引号中。这些双引号是必要的，因为赋值给这些这些变量的数据中可能包含空格。
最后一步是将新的 `default.conf` 文件复制到新 vault 中以完成 vault 配置。

## 删除备份

到这里，你可能在想：“好了，这个脚本什么时候结束？”好吧，这之后还有一个主题。在本节中，我们想要从 Dirvish 备份脚本中删除一个 vault/hostname。做到此点的唯一方法是删除 vault 目录及其所有内容。`delete_backup` 函数的工作由一条命令完成：

```bash
rm -fr $VAULT_ID
```

在开始删除目录及其所有内容之前，我们需要进行一些合理检查以确保我们不会破坏某些东西。查看列表 27-22 中的 `delete_backup` 函数，我们将在最后介绍细节。

```bash
delete_backup ()
{
  clear
echo -e "\n\n\tREMOVE A SERVER FROM DIRVISH BACKUPS\n"
echo -e "\n\nEnter the Host to Remove from Dirvish Backups: \c"
read H
BANK_LIST=$(parse_conf)
```

列表 27-22 `delete_backup` 函数

## 第三部分 用于系统管理员的脚本

```bash
for P in $BANK_LIST
do
  VAULT_ID=$(find $P -type d -name "$H")
  if [ ! -z "$VAULT_ID" ]; then
    STOP=0
    until (( STOP == 1 ))
    do
      echo -e "\nRemove Backup Vault $H from the Dirvish Server? (y/n):\c"
      read ANS
      case $ANS in
        y|Y) echo -e "\nRemoving Backup Vault for $H from Dirvish Backups...\c"
          rm -fr "$VAULT_ID"
          echo -e "\ntBackup Vault Removed..Press Enter to Continue...\c"
            read KEY
            STOP=1
            :;
        n|N) echo -e "\ntVault Removal Canceled..Press Enter to Continue...\c"
            read KEY
            STOP=1
            continue
        **) echo -e "\ntInvalid Entry..."
          :;
      esac
    done
  fi
done
```

**列表 27-22（续）**

我们在列表 27-22 中开始 `delete_backup` 函数，通过清除屏幕并显示屏幕头。我们询问用户要删除的主机名/vault，并在所有 banks 中搜索指定的主机名。如果我们找到了 vault，我们会要求用户确认删除它（“确定吗..”）。如果用户响应 y 或 Y，我们就运行 `rm -fr "$VAULT_ID"`，这将从 Dirvish 备份服务器上删除该 vault。

## 管理 Dirvish 备份 Banks

我编写此脚本时允许修改 `master.conf` 文件，就像我们修改摘要文件使备份镜像过期一样。`manage_banks` 函数太长了，这里不再重复。详细信息请参见列表 27-24 中的 `dirvish_ctrl` 脚本。

## 第 27 章 使用 Dirvish 和 rsync 创建快照类型备份 891

我们从清除屏幕并显示屏幕头开始 `manage_banks` 函数。下一步是显示 Dirvish 配置文件 `master.conf` 中的所有 banks。如果当前没有定义任何 banks（例如在全新的 Dirvish 安装中），我们会告知用户。然后我们显示管理 Dirvish 备份 banks。此菜单代码显示在此：

```bash
echo "\n1" Add a New Backup Bank
echo "\n2" Delete a Backup Bank
echo "\n3" Return to the Previous Menu
echo "\nSelect an Option: \c"
```

我们的选项是添加新的 Dirvish 备份或删除当前定义的备份 bank。添加新的 Dirvish 备份 bank 是一个两步骤的过程。首先，我们在 Dirvish 主配置文件 `master.conf` 中定义新 bank。然后，我们需要在系统上为新 bank 创建目录。

> 注意：为每个 bank 创建单独的文件系统始终是一个好主意。你也可以创建一个大文件系统并让不同的 bank 居住其中。

## 添加新的 Dirvish 备份 bank

通过遍历 `master.conf` 找到最后定义的 bank。在循环中将值赋值给 `LAST_ENTRY`。循环完成后，我们使用 `sed` 将新 bank添加到 `master.conf`：

```bash
for B in $BANK_LIST
do
  (( COUNT++ ))
  LAST_ENTRY=$B
done
```

如果 `$COUNT` 等于 0，则：

```bash
sed -i "/$LAST_ENTRY/a $B" master.conf
fi
```

## 删除 Dirvish 备份 bank

要从 `master.conf` 删除 bank，我们使用带有 `-v` 参数的 `grep`。`-v` 告诉 `grep` 列出模式以外的所有内容。然后我们将修改后的文件复制到 `master.conf`。在删除包含镜像的实际目录结构之前，我们询问用户。

```bash
cat master.conf | grep -v "$B" > master.conf.bak
cp -p master.conf.bak master.conf
if [ -d $B ]; then
  echo -e "\nWant to Remove $B? (y/n):\c"
  read ANS
  case $ANS in
    y|Y) rm -rf "$B"
      if [ $? -eq 0 ]; then
        echo -e "\nB Removed Successfully"
      else
        echo -e "\nERROR: Remove $B Failed"
      fi
      ;;
    n|N) echo -e "\nskipping $B Removal"
      ;;
    *) echo -e "\nInvalid Input..."
      ;;
  esac
fi
```
