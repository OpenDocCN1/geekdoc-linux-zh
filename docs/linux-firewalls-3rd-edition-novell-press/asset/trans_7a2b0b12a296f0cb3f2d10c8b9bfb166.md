
## 附录 B：防火墙示例与支持脚本

```bash
$IPT --policy FORWARD ACCEPT
$IPT -t nat --policy PREROUTING ACCEPT
$IPT -t nat --policy OUTPUT ACCEPT
$IPT -t nat --policy POSTROUTING ACCEPT
$IPT -t mangle --policy PREROUTING ACCEPT
$IPT -t mangle --policy OUTPUT ACCEPT
if [ "$1" = "stop" ]
then
echo "Firewall completely stopped! WARNING: THIS HOST HAS NO FIREWALL RUNNING."
exit 0
fi

# Unlimited traffic on the loopback interface
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT

# Set the default policy to drop
$IPT --policy INPUT DROP
$IPT --policy OUTPUT DROP
$IPT --policy FORWARD DROP
$IPT -t nat --policy PREROUTING DROP
$IPT -t nat --policy OUTPUT DROP
$IPT -t nat --policy POSTROUTING DROP
$IPT -t mangle --policy PREROUTING DROP
$IPT -t mangle --policy OUTPUT DROP

# Create the user-defined chains
for i in $USER_CHAINS; do
    $IPT -N $i
done

#######################################################
# DNS Caching Name Server (query to remote, primary server)
$IPT -A EXT-output -p udp --sport 53 --dport 53 \
    -j local-dns-server-query
$IPT -A EXT-input -p udp --sport 53 --dport 53 \
    -j remote-dns-server-response
# DNS Caching Name Server (query to remote server over TCP)
$IPT -A EXT-output -p tcp \
    --sport $UNPRIVPORTS --dport 53 \
    -j local-dns-server-query

$IPT -A EXT-input -p tcp ! --syn \
        --sport 53 --dport $UNPRIVPORTS \
        -j remote-dns-server-response

################################################################
# DNS Forwarding Name Server or Client requests

if [ "$CONNECTION_TRACKING" = "1" ]; then
        $IPT -A local-dns-server-query \
                -d $NAMESERVER_1 \
                -m state --state NEW -j ACCEPT
        $IPT -A local-dns-server-query \
                -d $NAMESERVER_2 \
                -m state --state NEW -j ACCEPT
        $IPT -A local-dns-server-query \
                -d $NAMESERVER_3 \
                -m state --state NEW -j ACCEPT
fi

$IPT -A local-dns-server-query \
        -d $NAMESERVER_1 -j ACCEPT
$IPT -A local-dns-server-query \
        -d $NAMESERVER_2 -j ACCEPT
$IPT -A local-dns-server-query \
        -d $NAMESERVER_3 -j ACCEPT

# DNS server responses to local requests
$IPT -A remote-dns-server-response \
        -s $NAMESERVER_1 -j ACCEPT
$IPT -A remote-dns-server-response \
        -s $NAMESERVER_2 -j ACCEPT
$IPT -A remote-dns-server-response \
        -s $NAMESERVER_3 -j ACCEPT

################################################################
# Local TCP client, remote server
$IPT -A EXT-output -p tcp \
        --sport $UNPRIVPORTS \
        -j local-tcp-client-request

$IPT -A EXT-input -p tcp ! --syn \
    --dport $UNPRIVPORTS \
    -j remote-tcp-server-response

##############################################################
# Local TCP client output and remote server input chains
# SSH client
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A local-tcp-client-request -p tcp \
    -d <selected host> --dport 22 \
    -m state --state NEW \
    -j ACCEPT
fi
$IPT -A local-tcp-client-request -p tcp \
    -d <selected host> --dport 22 \
    -j ACCEPT
$IPT -A remote-tcp-server-response -p tcp ! --syn \
    -s <selected host> --sport 22 \
    -j ACCEPT

#...........................................................................
# Client rules for HTTP, HTTPS, AUTH, and FTP control requests
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A local-tcp-client-request -p tcp \
    -m multiport --destination-port 80,443,21 \
    -m state --state NEW \
    -j ACCEPT
fi
$IPT -A local-tcp-client-request -p tcp \
    -m multiport --destination-port 80,443,21 \
    -j ACCEPT
$IPT -A remote-tcp-server-response -p tcp \
    -m multiport --source-port 80,443,21 ! --syn \
    -j ACCEPT

#...........................................................................
# POP client
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A local-tcp-client-request -p tcp \
    -d $POP_SERVER --dport 110 \
    -m state --state NEW \
    -j ACCEPT
fi
$IPT -A local-tcp-client-request -p tcp \
    -d $POP_SERVER --dport 110 \
    -j ACCEPT
$IPT -A remote-tcp-server-response -p tcp ! --syn \
    -s $POP_SERVER --sport 110 \
    -j ACCEPT

#........................................................
# SMTP mail client
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A local-tcp-client-request -p tcp \
    -d $MAIL_SERVER --dport 25 \
    -m state --state NEW \
    -j ACCEPT
fi
$IPT -A local-tcp-client-request -p tcp \
    -d $MAIL_SERVER --dport 25 \
    -j ACCEPT
$IPT -A remote-tcp-server-response -p tcp ! --syn \
    -s $MAIL_SERVER --sport 25 \
    -j ACCEPT

#........................................................
# Usenet news client
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A local-tcp-client-request -p tcp \
    -d $NEWS_SERVER --dport 119 \
    -m state --state NEW \
    -j ACCEPT
fi
$IPT -A local-tcp-client-request -p tcp \
    -d $NEWS_SERVER --dport 119 \
    -j ACCEPT
$IPT -A remote-tcp-server-response -p tcp ! --syn \
      -s $NEWS_SERVER --sport 119 \
      -j ACCEPT

#.......................................................................
# FTP client - passive mode data channel connection
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A local-tcp-client-request -p tcp \
         --dport $UNPRIVPORTS \
         -m state --state NEW \
         -j ACCEPT
fi
$IPT -A local-tcp-client-request -p tcp \
     --dport $UNPRIVPORTS -j ACCEPT
$IPT -A remote-tcp-server-response -p tcp ! --syn \
     --sport $UNPRIVPORTS -j ACCEPT

############################################################
# Local TCP server, remote client
$IPT -A EXT-input -p tcp \
     --sport $UNPRIVPORTS \
     -j remote-tcp-client-request
$IPT -A EXT-output -p tcp ! --syn \
     --dport $UNPRIVPORTS \
     -j local-tcp-server-response

# Kludge for incoming FTP data channel connections
# from remote servers using port mode.
# The state modules treat this connection as RELATED
# if the ip_conntrack_ftp module is loaded.
$IPT -A EXT-input -p tcp \
     --sport 20 --dport $UNPRIVPORTS \
     -j ACCEPT
$IPT -A EXT-output -p tcp ! --syn \
     --sport $UNPRIVPORTS --dport 20 \
     -j ACCEPT

################################################################################
# Remote TCP client input and local server output chains
# SSH server
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A remote-tcp-client-request -p tcp \
    -s <selected host> --destination-port 22 \
    -m state --state NEW \
    -j ACCEPT
fi
$IPT -A remote-tcp-client-request -p tcp \
    -s <selected host> --destination-port 22 \
    -j ACCEPT
$IPT -A local-tcp-server-response -p tcp ! --syn \
    -s <selected host> --source-port 22 \
    -j ACCEPT

#...............................................................................
# AUTH ident server
if [ "$ACCEPT_AUTH" = "0" ]; then
    $IPT -A remote-tcp-client-request -p tcp \
    --destination-port 113 \
    -j REJECT --reject-with tcp-reset
else
    $IPT -A remote-tcp-client-request -p tcp \
    --destination-port 113 \
    -j ACCEPT
    $IPT -A local-tcp-server-response -p tcp ! --syn \
    --source-port 113 \
    -j ACCEPT
fi

################################################################################
# Local UDP client, remote server
$IPT -A EXT-output -p udp \
--sport $UNPRIVPORTS \
-j local-udp-client-request
$IPT -A EXT-input -p udp \
--dport $UNPRIVPORTS \
-j remote-udp-server-response

################################################
# NTP time client
if [ "$CONNECTION_TRACKING" = "1" ]; then
    $IPT -A local-udp-client-request -p udp \
         -d $TIME_SERVER --dport 123 \
         -m state --state NEW \
         -j ACCEPT
fi
$IPT -A local-udp-client-request -p udp \
     -d $TIME_SERVER --dport 123 \
     -j ACCEPT
$IPT -A remote-udp-server-response -p udp \
     -s $TIME_SERVER --sport 123 \
     -j ACCEPT

################################################
# ICMP
$IPT -A EXT-input -p icmp -j EXT-icmp-in
$IPT -A EXT-output -p icmp -j EXT-icmp-out

################################################
# ICMP traffic
# Log and drop initial ICMP fragments
$IPT -A EXT-icmp-in --fragment -j LOG \
     --log-prefix "Fragmented incoming ICMP: "
$IPT -A EXT-icmp-in --fragment -j DROP
$IPT -A EXT-icmp-out --fragment -j LOG \
     --log-prefix "Fragmented outgoing ICMP: "
$IPT -A EXT-icmp-out --fragment -j DROP

# Outgoing ping
if [ "$CONNECTION_TRACKING" = "1" ]; then
  $IPT -A EXT-icmp-out -p icmp \
       -i icmp-type echo-request \
       -m state --state NEW \
       -j ACCEPT
fi
```

