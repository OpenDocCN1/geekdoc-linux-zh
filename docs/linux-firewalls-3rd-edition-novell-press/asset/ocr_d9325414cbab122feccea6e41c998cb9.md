```
# ####################################################################
# Filtering the AUTH User Identification Service (TCP Port 113)

# Outgoing Local Client Requests to Remote Servers

$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport SUNPRIVPORTS \
-dport 113 -m state --state NEW -j ACCEPT
fi
$IPT -A OUTPUT -o $INTERNET -p tcp \
-s $IPADDR --sport $UNPRIVPORTS \
-dport 113 -j ACCEPT

$IPT -A INPUT -i $INTERNET -p tcp ! --syn \
--sport 113 \
-d $IPADDR -dport SUNPRIVPORTS -j ACCEPT

# .........................
# Incoming Remote Client Requests to Local Servers

if [ "$ACCEPT_AUTH" = "1" ]; then
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS \
-d $IPADDR -dport 113 \
-m state --state NEW -j ACCEPT

fi
$IPT -A INPUT -i $INTERNET -p tcp \
--sport $UNPRIVPORTS
-d $IPADDR -dport 113 -j ACCEPT
$IPT -A OUTPUT -o $INTERNET -p tcp ! --syn \
-s $IPADDR --sport 113 \
-dport $UNPRIVPORTS -j ACCEPT
else
$IPT -A INPUT -i $INTERNET -p tcp \
--sport SUNPRIVPORTS \
-d $IPADDR -dport 113 -j REJECT --reject-with tcp-reset
fi
# ####################################################################
# Sending Mail to Any External Mail Server
# Use -d $MAIL_SERVER" if an ISP mail gateway is used instead
```