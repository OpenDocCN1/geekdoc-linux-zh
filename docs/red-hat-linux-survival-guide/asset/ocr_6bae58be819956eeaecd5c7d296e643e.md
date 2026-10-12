![](bbox=[0.07, 0.15, 0.18, 0.25])

If you enable this you cannot perform network packet filtering.

```
Forwarding between high speed interfaces (CONFIG_NET_HW_FLOWCONTROL) [N/y/?]
```

Enable this if you wish to turn on network hardware-based bandwidth throttling in a fast network.

```
QoS and/or fair queueing (CONFIG_NET_SCHED) [N/y/?]
```

This option should be turned on if you wish to enable the fair queuing scheme to control Quality of Service (QoS) during peak network traffic. Enabling this will allow you to choose different algorithm for prioritizing packets of different types when there are too many to handle. I recommend enabling it. If you do enable it you will have to select schedulers options from the following selection:

+   - CBQ packet scheduler (CONFIG_NET_SCH_CBQ) [N/y/m/?] (NEW)
+   - CSZ packet scheduler (CONFIG_NET_SCH_CSZ) [N/y/m/?]
+   - The simplest PRIO pseudoscheduler (CONFIG_NET_SCH_PRIO) [N/y/m/?] (NEW)
+   - RED queue (CONFIG_NET_SCH_RED) [N/y/m/?] (NEW)
+   - SFQ queue (CONFIG_NET_SCH_SFQ) [N/y/m/?] (NEW)
+   - TEQL queue (CONFIG_NET_SCH_TEQL) [N/y/m/?] (NEW)
+   - TBF queue (CONFIG_NET_SCH_TBF) [N/y/m/?] (NEW)
+   - GRED queue (CONFIG_NET_SCH_GRED) [N/y/m/?] (NEW)
+   - Diffserv field marker (CONFIG_NET_SCH_DSMARK) [N/y/m/?] (NEW)
+   - Rate estimator (CONFIG_NET_ESTIMATOR) [N/y/?] (NEW)
+   - Packet classifier API (CONFIG_NET_CLS) [N/y/?] (NEW)

Use the ? option to learn about the different schedulers and use the one that you feel is most appropriate for your network.

# Telephony options

If you wish to enable telephony support, choose yes here. Most users will not need to enable support for telephony devices.

```
Linux telephony support (CONFIG_PHONE) [N/y/m/?]
```