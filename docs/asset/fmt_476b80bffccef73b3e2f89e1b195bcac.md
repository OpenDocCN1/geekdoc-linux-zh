
在安装到启动盘和根软盘的文件中，其中一个是为 `root` 提供的 `.bashrc` 文件，其中包含名为 `setup` 的函数的定义。该函数会提示用户输入要安装机器使用的主机名，然后执行配置具有该名称和相关 IP 地址的以太网接口所需的步骤。完成后，它会为需要访问的网络建立路由，并启动 `inetd` 和 `syslog` 守护进程。此函数的定义是网络特定的，因此使用我使用的那个对您没有帮助，但通过检查该函数所采取的步骤，您可以轻松地将其修改为适用于您的网络。列表 3.1 中的代码显示了我启动软盘上 `.bashrc` 的内容，其中实现了 `setup` 函数。

### 列表 3.1 `/root/.bashrc` 中 `setup` 函数的实现

```
# defines the setup function used to establish network connectivity

setup () {
# Function to set up network connectivity for installation

# Prompt the user for the type of NIC to use
echo "Drivers are available for the following NICS:"
echo " 1 -- 3Com 509 10Mbit (3c509)"
echo " 2 -- Kingston KNE100TX or Digital DE500 (de4x5)"
echo " 3 -- Intel EtherExpress Pro/100+ (eepro100)"
echo -n "Enter the number for the appropriate driver to load  "
read nic

echo ""
case $nic in
1)    echo -n "Loading 3c509 module..."
      /sbin/insmod 3c509
      LOADED=`/sbin/lsmod | grep 3c509`
      if [ "$LOADED" != "" ]; then
          echo "done."
      else
          echo "failed...aborting."
          return
      fi
      ;;
2)    echo "Loading de4x5 module..."
      /sbin/insmod de4x5
      LOADED=`/sbin/lsmod | grep de4x5`
      if [ "$LOADED" != "" ]; then
          echo "done."
      else
          echo "failed...aborting."
          return
      fi
      ;;
3)    echo "Loading eepro100 module..."
      /sbin/insmod eepro100
      LOADED=`/sbin/lsmod | grep eepro100`
      if [ "$LOADED" != "" ]; then
          echo "done."
      else
          echo "failed...aborting."
          return
      fi
      ;;
*) echo "Invalid response...exiting"
return
;;

DONE=N

while [ "$DONE" != "Y" ]; do
# Now that the module is loaded, prompt for the hostname to use
echo ""
echo -n "Enter the fully qualified hostname to use: "
read hname

HNAME=`echo $hname | cut -d . -f1`
HIP=`grep "$HNAME" /etc/hosts | cut -f1`

if [ "$HIP" = "" ]; then
echo ""
echo -n "$hname not found in /etc/hosts...use anyways (y/n)? "
read ans

if [ "$ans" = "y" -o "$ans" = "Y" ]; then
echo -n "Enter the IP address for $hname: "
read HIP
fi
else
echo ""
echo -n "$HIP found for $hname...is this correct (y/n)? "
read ans
fi

if [ "$ans" = "y" -o "$ans" = "Y" ]; then
DONE=Y
fi
done

# We now have a hostname and IP address. Determine from them the
# appropriate routes to setup and start the inetd.
hostname $hname
echo $hname >>/etc/HOSTNAME

export HOSTNAME=$hname

DEV="192.168.50"

ATO_DEV=`echo $HIP | grep $DEV`

if [ "$ATO_DEV" != "" ]; then
ifconfig eth0 $HIP broadcast 192.168.50.255 netmask 255.255.255.0
route add -net 192.168.50.0 netmask 255.255.255.0 dev eth0
route add default gw 192.168.50.2 metric 1 dev eth0
echo ""
echo "Verify network setup by pinging quicksilver."
/usr/sbin/inetd
return
fi

echo "Unfamiliar network...establish network connectivity manually"
}
```

此 `setup` 函数对其必须位于启动软盘上的实用程序有自己的要求。所需命令如下

- `hostname`
- `cut`
- `grep`
- `insmod`
- `lsmod`
- `ifconfig`
- `route`
- `inetd`

这些命令用于加载网络卡的适当模块，根据用户提供的主机名确定机器的 IP 地址，并配置以太网接口以准备通过网络接收连接。

## 分区磁盘并创建文件系统

现在您已接入网络，其余工作可以远程完成。由于您已在启动软盘上包含 `sfdisk`，并且当前未使用硬盘，您现在可以对启动磁盘进行分区并创建继续安装所需的文件系统和交换空间。这是通过列表 3.2 中的脚本实现的，该脚本连接到您从软盘启动的机器，运行 `sfdisk` 命令在目标主机启动驱动器上创建分区，然后运行 `mke2fs` 在新分区上创建文件系统。此外，如果您指定创建交换分区，脚本将运行 `mkswap` 来初始化它。

### 列表 3.2 使用 `sfdisk` 远程分区硬盘的脚本
