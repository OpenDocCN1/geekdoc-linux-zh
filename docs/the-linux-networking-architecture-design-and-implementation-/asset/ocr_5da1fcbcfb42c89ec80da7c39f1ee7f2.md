# 12.4 Implementation 217

sends the first configuration message over its designated port, the bridge 2 will check for whether it is better than the stored configuration. Such would not be the case in this example, so bridge 2 would return a configuration message with its own values. The information in this message would be better than the configuration stored on port 2 in bridge 3. Consequently, bridge 2 would run the spanning-tree algorithm. Port 1 would remain the root, but port 2 would no longer be a designated port and would be put into the blocking state. (See Figure 12–21.)

**Timer Handling** Each bridge has a function, br_tick(), to handle timers. This section describes the five defined timers. To implement them, only one timer of the type timer_list is used. This is the variable in each net_bridge structure.

The timer is invoked every second (expires = jiffies + H) This causes the function br_tick to be invoked each time. This function defines the behavior of the timers in the following list. Whether a timer is expired for each timer (br_check_timers()). In addition, the timers are incremented. The appropriate behavior is invoked as soon as a timer expires.

Hold timer: The hold timer starts after the configuration BPDU has been sent. When it is active, no configuration BPDU can be sent over the same port. The hold timer expires when its value reaches or exceeds the stored hold_time. Then the function br_transmit_config() is invoked, if no BPDU has been sent. Once it expires, the hold timer is not restarted. It is explicitly stopped when a port is disabled.

GC timer: The garbage collection timer does cleanup in the forwarding table. It checks periodically (gc_interval) on whether there are old entries in the forwarding table. If there are, then these entries are deleted, to respond to moving stations. In addition, this cleanup prevents the forwarding table

![](bbox=[0.145, 0.631, 0.854, 0.915])

FIGURE 12–21
Configuration for LAN 3.