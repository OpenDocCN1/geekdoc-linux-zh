+   2. If directory /etc/dhcpd doesn't exist, create it:
+   `mkdir /etc/dhcpd`

+   3. Make a link from /etc/dhcpd/resolv.conf to /etc/resolv.conf:
+   `ln -s /etc/dhcpd/resolv.conf /etc/resolv.conf`

If that doesn't work, try this (fix suggested by Nothing <nothing@cc.gatech.edu>, with a little amendment by Henrik Stoerner).

This last step I had to perform only because my dhcpd didn't create an /etc/dhcpd/resolv.conf. In /etc/sysconfig/network-scripts/ifup; I made the following changes (which are a very poor hack, but they work for me):

```
elif [ "$BOOTPROTO" = dhcp -a "$ISALIAS" = no ]; then
    echo -n "Using DHCP for $(DEVICE)..."
    /sbin/dhcpd -c /etc/sysconfig/.........
    echo "echo $! .........

if [ -f /var/run/dhcp-wait-$(DEVICE).pid ]; then

^ ^

echo 'failed.'
exit 1
```

I changed this to:

```
elif [ "$BOOTPROTO" = dhcp -a "$ISALIAS" = no ]; then
    echo -n "Using DHCP for $(DEVICE)..."
    /sbin/dhcpd
    echo "echo $! ...............

if [ ! -f /var/run/dhcp-wait-$(DEVICE).pid ]; then
^^^^^^

echo 'failed.'
exit 1
```

Notice the ! (bang) in if [ ! -f /var/run/dhcp-wait-$(DEVICE).pid ];
Now sit back and enjoy.