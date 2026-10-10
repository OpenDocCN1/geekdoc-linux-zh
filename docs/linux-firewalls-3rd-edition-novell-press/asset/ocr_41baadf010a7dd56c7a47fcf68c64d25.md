```
`
            -j ACCEPT
fi

$IPT -A local-tcp-client-request -p tcp \
-d $POP3_SERVER --dport 110 \
-j ACCEPT

$IPT -A remote-tcp-server-response -p tcp ! --syn \
-s $POP3_SERVER --sport 110 \
-j ACCEPT

# SMTP mail client
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A local-tcp-client-request -p tcp \
-d $SMTP_SERVER --dport 25 \
-m state --state NEW \
-j ACCEPT
fi

$IPT -A local-tcp-client-request -p tcp \
-d $SMTP_SERVER --dport 25 \
-j ACCEPT

$IPT -A remote-tcp-server-response -p tcp ! --syn \
-s $SMTP_SERVER --sport 25 \
-j ACCEPT

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

# FTP client - passive mode data channel connection
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A local-tcp-client-request -p tcp \
--dport SUNPORTS \

```