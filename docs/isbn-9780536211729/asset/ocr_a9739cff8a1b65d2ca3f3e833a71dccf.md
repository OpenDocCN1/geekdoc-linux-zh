```
file /proc/[0-9]*/exe

will list processes.
```

5. Sometimes /bin/login is replaced with one that has a "back door" that allows a cracker to become root by entering some word in place of an account listed in /etc/passwd.

# 12.3 Drop the Modems, Network, Printers, and System

Once you have detected that your system has been broken into, you must decide how much data to gather on the intrusion before stopping further damage. It is assumed that you already have gathered as much data as you dare by this point. Now you need to get the intruder out of your system. There are two parts to this. The first is preventing him from accessing your system, and I will address that here. (Later you need to remove what he has left behind in the way of compromised programs and plug security holes.)

Many system administrators forget that the most effective way to throw the intruder out is to sever the connections between the computer and the outside world. For most, this means disconnection from the network and modems.

> You should plan in advance for your response to an intrusion, because you will want to act quickly when an intrusion is discovered. A formal Security Procedures or Intrusion Response manual is recommended. Writing this document in advance is valuable because in the "heat of battle" you might not have the luxury of time nor be able to think as clearly.

This is why every pilot carries an Emergency Procedures document on his aircraft that lists the responses to common emergencies that have been thought out carefully in advance and are based on past experiences. On your next airline flight, on the way out, you might ask the flight crew to show you theirs. It will be instructional.

In many cases, the fast way to sever connectivity is to disconnect the modems from either the phone lines or electrical power. For a small setup, simply unplugging the phone cable from the modem or phone jack will do fine. I do this when I am under attack. For larger setups, having all the modems' power plugs in one or two power strips or UPS (Uninterruptible Power Supply) units will allow throwing one or two power switches to turn them off. This is easier than unplugging lots of phone cables and then later trying to figure out which one went where. (Having two sets of power strips or UPS units provides redundancy.)