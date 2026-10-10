
# 如果两个值的之差小于 35，则更新 dhcpc

```bash
if [ $New_time` -lt $SECONDS ]
then
    #在 /etc/dhcpc/dhcpcd-$IFACE.info 中获取 IP 地址
    grep -h 'IPADDR' $DHCP_INFO > /tmp/IP_Found 2>/dev/null
    if [ -s /tmp/IP_Found ]
    then
        sed '/^\*/=//' < /tmp/IP_Found > /tmp/New_IP
        IP_ADDRESS=`cat /tmp/New_IP`
    else
        exit 1
    fi
    #在 /etc/dhcpc/resolv.conf 中获取域名
    grep -i 'DOMAIN' $DHCP_INFO > /tmp/Domain_Found 2>/dev/null
    if [ -s /tmp/Domain_Found ]
    then
        sed 's/DOMAIN=//' < /tmp/Domain_Found > /tmp/New_Domain
        DOMAIN_NAME=`cat /tmp/New_Domain`
    else
        exit 1
    fi
    if [ -e $HOSTNAME_FILE ]
    then
        #在 /etc/hostname 中获取主机名
        HOST_NAME=`cat $HOSTNAME_FILE`
    else
        exit 1
    fi
    #查看 /etc/hosts 文件，如果存在...
    if [ -s $HOSTS_FILE ]
    then
        grep -v $IP_ADDRESS $HOSTS_FILE > /tmp/Host_File 2>/dev/null
        #进入 /etc/hosts 文件，注释掉
        #当前未被使用的 IP 地址
        if [ -v # /tmp/Host_File ]
        then
            grep -v '#' /tmp/Host_File > /tmp/Hosts 2>/dev/null
            if [ -s /tmp/Hosts ]
            then
                sed 's/^\./ # &/' /tmp/Hosts > $HOSTS_FILE
            fi
        fi
    else
        exit 1
    fi
    # 取消 /etc/hosts 文件中显示 "localhost" 的行的注释
    grep -i "localhost" /etc/hosts > /tmp/find_local
    if [ -s /tmp/find_local ]
    then
        grep -i "#*" /tmp/find_local > /tmp/find_host
        if [ -s /tmp/find_host ]
        then
            old_local=$(cat /tmp/find_local)
            sed -e "s/^.*/*/" < /tmp/find_local > /tmp/tmp_local
            sed -e "s/^.*/*/" < /tmp/tmp_local > /tmp/kate3
            new_local=$(cat /tmp/kate3)
            sed -e "s/$old_local/$new_local/*" < /etc/hosts > /tmp/hosts_file
            mv /tmp/hosts_file /etc/hosts
        else
            echo "已经取消注释了!"
        fi
    else
        echo "它不存在"
    fi
    grep -h $IP_ADDRESS $HOSTS_FILE > /tmp/tmp_IP 2>/dev/null
    if [ -s /tmp/tmp_IP ]
    then
        echo "正在检查 IP 地址是否存在..."
    else
        #将新的 IP 地址、主机名和
        #域名写入 /etc/hosts 文件。
        echo $IP_ADDRESS "$HOST_NAME.$DOMAIN_NAME **" $HOST_NAME >> "$HOSTS_FILE"
    fi
    else
        echo $IP_ADDRESS "$HOST_NAME.$DOMAIN_NAME ** $HOST_NAME >> "$HOSTS_FILE"
    fi
    else
        echo "抱歉，dhcpcd-$IFACE.info 文件未更新!"
    fi
    else
        echo "DHCP 目前未在运行..."
        exit 1
    fi
    rm -rf /tmp/Host_File /tmp/IP_Found /tmp/New_IP /tmp/tmp_IP /tmp/tmp_Domain
    rm -rf /tmp/Hosts /tmp/New_Domain /tmp/Found_DHCP /tmp/Domain_Found
    rm -rf /tmp/kate/ /tmp/find_local /tmp/find_host /tmp/tmp_local
}
```

## 附录 D. 初始化脚本

```bash
#################### 主函数 #######################
test -f $DAEMON || exit 0
# 测试是否为 >2.0 内核
case '`uname -r`' in
  2.0.*)
    echo "在 \`uname -r\` 内核上跳过 dhcpcd-sv"
    exit 0
esac
# 加载我们的配置文件，如果存在的话
if [ -f /etc/dhcpcd/config ]
then
  source /etc/dhcpcd/config
fi
case "$1" in
start)
  if [ "$IFACE" = "none" ]; then
    echo "DHCP 客户端守护进程已禁用"
    exit
  fi
  echo ""
  echo "启动 DHCP 客户端守护进程: dhcpcd"
  start-stop-daemon --start --quiet --exec $DAEMON -- $IFACE
  Update_Info
  NetBiosNode_Update
  NetBiosName_Update
  echo "."
  restart)
  echo ""
  echo "正在重启 DHCP 客户端: "
  start-stop-daemon --stop --quiet --exec $DAEMON
  rm -f /var/run/dhcpcd-eth0.pid
  echo -n "停止"
  start-stop-daemon --start --quiet --exec $DAEMON -- $IFACE
  Update_Info
  NetBiosNode_Update
  NetBiosName_Update
  echo "重启完成。"
  force-reload)
  echo "/etc/init.d/$NAME: 重载尚未实现"
  ;;
  stop() {
    echo "停止守护进程: dhcpcd"
    start-stop-daemon --stop --quiet --exec $DAEMON
    rm -f /var/run/dhcpcd-eth0.pid
    echo "."
  }
  echo "用法: /etc/init.d/$NAME (start|stop)"
  exit 1
  ;;
esac
exit 0
```

### dial

此脚本在需要连接外部时启动 `dial` 守护进程。该脚本的之处在于它引用了命名管道。命名管道是一种在进程间传输数据的特殊文件类型。有时使用 FIFO 而不是命名管道；FIFO 代表输入输出。由于 `dial` 需要命名管道才能工作，脚本在尝试启动之前会检查其是否存在。
