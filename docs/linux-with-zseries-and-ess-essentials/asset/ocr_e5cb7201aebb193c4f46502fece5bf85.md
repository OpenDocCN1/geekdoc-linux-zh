![](bbox=[0.22, 0.09, 0.9, 0.5])

Figure 6-3  PPRC volume states - synchronous mode of operation

# Copying PPRC secondary volumes

A PPRC secondary volume can be a FlashCopy primary volume. This allows you, for example, to produce a consistent point-in-time tertiary copy of the mirror volume while it is suspended. With PPRC V2 you can perform Asynchronous Cascading PPRC, whereby a (synchronous) PPRC secondary volume can simultaneously serve as the PPRC primary volume for a PPRC-XD relationship to a remote site. This provides the capability for a three-site PPRC configuration.

# 6.3 PPRC Extended Distance (PPRC-XD)

Peer-to-Peer Remote Copy Extended Distance (PPRC-XD) is a non-synchronous long-distance copy option for both open systems and zSeries servers. PPRC-XD can operate at distances well beyond the 103 km maximum supported distance for synchronous PPRC. It is an excellent solution for:

+   - Data copy
- Data migration
- Off-site backup
- Transmission of data base logs
- Application recovery solutions based on periodic point-in-time copies of data

In PPRC-XD, the primary volumes updates are mirrored to the secondary volumes in a non-synchronous operation while the application is running. Due to the non-synchronous transmission of the updates, the write operations at the primary site (and thus the application's response time) are not affected by any transmission delay. When PPRC-XD