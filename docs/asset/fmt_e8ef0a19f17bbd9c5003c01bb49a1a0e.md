
```
do
    say "Do you want to IPL Linux from minidisk 100? y/n"
    parse upper pull answer.
    if (answer = 'Y') then 'CP IPL 100'
end /j* else */
```

# Linux 源代码

此节列出了与本书相关的 Linux 源代码。以下是**克隆脚本**。

## 获取和使用网络材料

本书的 PDF 可以在互联网上获取：
http://www.redbooks.ibm.com/abstracts/sg247492.html

与本书相关的文件位于一个压缩 tar 包中：
ftp://www.redbooks.ibm.com/redbooks/SG24492

将 tar 文件下载到你的 NFS 服务器，并按照第 7.2 页的“Copying files to controller”部分进行操作。解压文件后，将得到一个名为 `virt-clone` 的目录，其中包含以下文件：

- `README.txt`
- `clone-0-s390.rpm` 将黄金镜像克隆到目标目录的脚本，用于 `z/VM/sbin`

## 克隆脚本

```bash
#!/bin/sh

# clone.sh 是一个克隆 Linux 镜像的脚本。它使用 vmcp 将# 消息传递给 z/VM 系统并在镜像克隆后修改配置文件。
# 脚本读取 /etc/sysconfig/clone 进行自定义。
# 关于此脚本如何工作，请参阅书籍：Virtualization Cookbook for RHEL
# 以及网站：http://www.redbooks.com/abstracts/sg24722.html
# 本程序按原样提供，不提供任何形式的保证或条件，
# 无论是明示还是隐含的，包括对于侵权的、适用性或针对特定用途的保证。接收者或任何贡献者均不对任何直接、间接、偶然的损害承担责任，无论是由于使用或分发程序或行使授予此者的任何权利而引起的损害（包括由于疏忽或其他原因引起的）。
# 必须是小写！

MASTER_LINK=
CLONE_LINK=

function help
    # 提供帮助
    {
        echo "usage: clone [-v] masterGuestID cloneID [rootMinisk minidisk]"
        echo "Switches"
        echo -v 详细输出
        echo "Required"
        echo masterGuestID 要克隆的 z/VM 用户 ID
        echo cloneID 要克隆到的 z/VM 用户 ID
        echo "Optional"
        echo rootMinisk 根文件系统的地址
        echo minidisk 应该复制的额外磁盘
        exit
    }

function cp_cmd
    # 打印 CP 命令并通过 cp_cmd 调用它
    # Arg-1: 要执行的 z/VM 命令
    # Return: z/VM 命令的返回码
    [ -VERBOSE ] && echo Invoking cp command: $0
    out=$(vmcp $2 2>&1)
    rc=$?
    # 从输出中提取 z/VM 错误代码
    if [ $rc -ne 0 ]; then
        rc=$(echo $out | grep Error | sed.*/)
        [ -z "$rc" ] && rc=1
    fi
    return $rc

function copy_key
    # 如果主机有 id_dsa_pub 文件，则将其添加到克隆的 authorized_keys 文件。
    {
        if [ -e /root/.ssh/id_dsa_pub ] then
            [ -d /mnt/clone/root/.ssh ] && mkdir -p /mnt/clone/root/.ssh/
            echo "# LNKINST" >> /mnt/clone/root/.ssh/authorized_keys
            cat /root/.ssh/id_dsa_pub >> /mnt/clone/root/.ssh/authorized_keys
            chmod 600 /mnt/clone/root/.ssh/authorized_keys
        fi
    }

function abort
    # 退出脚本并清理
    {
        umount_cloned_image
        set_offline CLONE_LINK
        set_offline MASTER_LINK
        unlink_one CLONE_LINK
        unlink_one $MASTER_LINK
        exit $1
    }

function get_target_info
    # 获取要克隆的 Linux ID 的 IP 和 DNS。此函数会检查 shared.conf 文件和特定目标 ID 的配置文件。如果值仍然缺失，将提示用户输入。
    {
        unset HOSTNAME
        [ -f /etc/clone/shared.conf ] && /etc/clone/shared.conf
        [ -f /etc/clone/${cloned_linux_id}.conf ] && /etc/clone/${cloned_linux_id}.conf
    }

shift drop the MasterGuestID
shift drop the GuestID
# 如果还有参数，用户必须在命令行上指定了 DASD。取消 DASD 中的任何内容（来自配置文件），
# 并设置 DASD 也=$DASD $1
# [ -z $0 ] && DASD=$0 && unset DASD_ROOT

# 循环遍历我们需要的所有值并双检它们是否存在。
# 如果不存在，我们将提示用户填写。
for v in HOSTNAME EPOCH ID GATEWAY NETMASK ID SUBCHANNELS SEARCHONDS NETTYPE DASD
do
  if [ -z "$v" ]; then
    [ "$PROMPT" = "y" ] && echo "Error: missing required value for $v" && exit 1
    [ -z "$first" ] && echo "Please enter ${cloned_linux_id}'s value for: " && first=1
    echo -n "$v:"
    read
    eval $v="\$input"
  export $v
  echo "$v" >> /etc/clone/${cloned_linux_id}.conf
done

fi
done

# 如果定义了 DASD 范围，则展开它

if [ -n "$DASD" ]; then
  split=$(echo $DASD | tr ',' '\n')
  DASD=**
  for s in $split
  do
    out=$(echo $s | grep \-)
    rc=$?
    [ $rc -ne 0 ] && DASD="$DASD-$(seq "$s" | $(echo $s | tr '\'-' '-' | tr '\n' ' '))
    [ $rc -ne 0 ] && DASD="$DASD-$(echo -n "$s")"
  done
  [ -n "$DASD_ROOT" ] && echo $DASD | sed "$/$DASD_ROOT//"
  DASD="$DASD_ROOT"
  # 假设如果没有指定 DASD_ROOT，则第一个 DASD 设备将
  # 作为根设备
  if [ -z "$DASD_ROOT" ]; then
    DASD_ROOT=$(echo $DASD | awk -F " " '{print $1}')
  fi
fi

# 从 FQDN 中提取带有任何 DNS 后缀的主机
target_host=$(echo $target_fqhost | awk -F " " '{print $1}')

# function dd_copy
# 使用 dd 命令拷贝一个设备，到

# 参数 1: 假设为离线的源 minidisk
```
