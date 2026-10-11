# Example 16-25 ipchains Firewall Start-up Script

```
#!/bin/sh
##
## *****Firewall Start-Up Script************
# chkconfig: 2345 9 91
# description: Activates/Deactivates ipchains firewall
#
# case "$1" in
start)
# Verify the existence of the rule base
if [ ! -x /etc/fw/rules ]; then
 echo "The ipchains script doesn't exist or isn't"
 echo "executable! Can't start the firewall. Be Afraid!"
 exit 1
fi
/etc/fw/rules
echo "Firewall is up."
;;
stop)
open)
/sbin/ipchains -F
/sbin/ipchains -P input ACCEPT
/sbin/ipchains -P output ACCEPT
/sbin/ipchains -P forward ACCEPT
echo "Firewall is down."
;;
save)
/sbin/ipchains-save > /etc/fw/rules
echo "Rules saved."
;;
*)
echo "Usage: /etc/rc.d/init.d/fwconfig [start|stop|clear|save]"
;;
esac
exit 0
```

# Building Your Firewall

In this section, we will explore a simple firewall scenario and go through a detailed look at building the rules for that scenario. This example is not intended to meet the needs of any particular environment, so use it at your own risk. The primary purpose of this section is to deepen your understanding of the way in which `ipchains` and IP masquerading work.

# Simple Internal Network

For our first example, we'll use the scenario described in Figure 16.2 on page 459. We provide a simplified diagram in Figure 16.3 to set the stage.
For simplicity, this example will use a static external IP address. This approach provides a nice example for an internal network that must be firewalled from the rest of an organization's intranet (just change Internet to