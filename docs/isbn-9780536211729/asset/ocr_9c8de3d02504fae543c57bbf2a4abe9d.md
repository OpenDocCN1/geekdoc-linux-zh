# 7.2.4 Resetting Default Policies and Stopping the Firewall

So far, the firewall has set some defaults that can be used regardless of the state of the Netfilter firewall. Before setting the default policies to DROP, I'll first reset the default policies to ACCEPT. This is useful for stopping the firewall completely, as you'll see shortly. These lines set the default policy:

```
# Reset the default policy
IPT --policy INPUT ACCEPT
IPT --policy OUTPUT ACCEPT
IPT --policy FORWARD ACCEPT
IPT -t nat --policy PREROUTING ACCEPT
IPT -t nat --policy OUTPUT ACCEPT
IPT -t nat --policy POSTROUTING ACCEPT
IPT -t mangle --policy PREROUTING ACCEPT
IPT -t mangle --policy OUTPUT ACCEPT
```

Here's a final addition to what I term to be the beginning of the firewall script, namely the code to enable the firewall to be stopped easily. This code placed before the previous code, when you call the script with an argument of "stop" the script will flush, clear, and reset the default policies and the firewall will effectively stop:

```
if [ "$1" = "stop" ]
then
echo "Firewall completely stopped! WARNING: THIS HOST HAS NO
FIREWALL RUNNING."
exit 0
fi
```

# 7.2.5 Enabling the loopback Interface

You need to enable unrestricted loopback traffic. This enables you to run any local network-based services that you—or that the system depends on—without having to worry getting all the firewall rules specified.

Local services on the loopback network interface. After the system boots, the system's default policy is to accept all packets. Flushing existing connections has no effect. However, if the firewall is being reinitialized and had previously used a deny-by-default policy, the drop policy would still be in effect. Without any acceptance rules, the loopback interface would still be inaccessible.

Because the loopback interface is a local, internal interface, the firewall can allow loopback traffic immediately.

```
# Unlimited traffic on the loopback interface
IPT -A INPUT -i lo -j ACCEPT
IPT -A OUTPUT -o lo -j ACCEPT
```