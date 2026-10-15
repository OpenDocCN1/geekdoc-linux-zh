# Dial Backup

Dial backup provides an alternate route to a network based on a network failure. The network failure can be determined based on an interface status or a condition reported by a network protocol, such as a network failure. Although not required, dial backup is usually used to back up a leased line connection.

Consider Figure 7.3. The Linux router, "sleepy," is connected to the router, "tired," via a fractional T1 line providing 256Kbps of bandwidth (without compression) for the dedicated connection.

![](bbox=[0.25, 0.38, 0.78, 0.55])

Figure 7.3 Dial backup network.

As shown in Figure 7.4, the leased line has failed. The backup connection has become active, providing continued connectivity between the sites.

![](bbox=[0.22, 0.7, 0.78, 0.85])

Figure 7.4 Dial backup network with failure.

# Bandwidth on Demand

Bandwidth on demand uses a dial-up connection to provide additional bandwidth to a network by adding the bandwidth of a dial up to the already existing connection through a load-balancing algorithm. The bandwidth on demand is triggered by a utilization threshold on the main link.

The PPP multilink protocol can be used to bundle multiple PPP links together and is defined in RFC 1990, "The PPP Multilink Protocol (MP)."