# **FIGURE 12.3** A Snort system can be placed at any of several locations to monitor network activity.

![](bbox=[0.28, 0.19, 0.8, 0.57])

> > Snort doesn't need an IP address to monitor network traffic. Thus, you can configure a dedicated Snort system with network drivers but without an IP address and use it to monitor network traffic. This configuration makes the Snort monitor very resistant to external attacks, because an attacker can't directly address the system. On the downside, you must use the Snort system's own console or an RS-232 serial link to it to monitor its activities.

# ## Using PortSentry

Another IDS is PortSentry ([http://sourceforge.net/projects/sentrytools/](http://sourceforge.net/projects/sentrytools/)). The basic idea behind PortSentry is similar to that of Snort, in the sense that both are designed to alert you to suspicious network activity. One critical difference is that PortSentry runs on individual computers to monitor access attempts to their own ports, whereas Snort can monitor an entire network. Another difference is that PortSentry can actively block network scans. In fact, in some sense PortSentry is more like a firewall than an IDS.