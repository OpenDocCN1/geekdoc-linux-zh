# Figure 14.4 The ODI driver setup for external card.

```
H:\ODI\NET.CFG:
Link Support
  Max Stacks 5
  buffers 10 4170
  mempool 4210

:: Note that this is a specialized NET.CFG for the WPO Gateway
:: application.
LINK DRIVER OSH39XR
  SPEED 16
  INT 5
  PORT 5A20
:: DMA doesn't work with PS/2's and Proteon 4/16 TR... set to 0.
  DMA 0
  MAX FRAME SIZE 4210
  CABLE STP
  DMACLOCK BUS
  FRAME TOKEN-RING_SNAP

Protocol: TCPIP
:: Please use your OWN addresses!
  ip_address      167.195.160.7
  ip_netmask      255.255.255.0
  ip_router       167.195.160.1
  tcp_sockets     24
  udp_sockets     8
  raw_sockets     1
  nb_sessions     4
  nb_commands     8
  nb_adapter      0
  nb_domain
  PATH            TCP_CFG H:\NET\tcp

H:\NET\TCP\RESOLV.CFG:
:: Please use your OWN domain and nameserver:
domain co.chatham.ga.us
nameserver 167.195.160.6
(Leave all other files in the Lan WP TCP directory as they are)
```