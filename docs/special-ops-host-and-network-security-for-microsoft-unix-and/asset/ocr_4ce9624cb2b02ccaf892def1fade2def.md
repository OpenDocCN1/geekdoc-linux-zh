# Inventory and Exposure of Corporate Assets · Chapter 2

# Figure 2.10 ToneLocLog

```
SYSLOG(Local): New message
18:00:03 ToneLoc <1.10 (Sep 20 1996)
18:00:03 Parameter set on Client-L2
18:00:03 Connection established (Ind.)
18:00:03 Bargain, Exp.
18:00:03 Timeout
18:00:03 Waiting for user
18:00:03 user logged 123456789
18:00:03 Installing service for Some
18:00:03 CARRIER
18:00:02 user exiting retry, ... some
18:00:02 Connection failed to 81516-ra
18:00:01 spawn current
18:00:01 Exit with error code 8
```

In the Found.log seen in Figure 2.11, a few identified systems are shown with their associated carrier banners. For the first number (123456890), the carrier banner appears below. These types of carrier banners should be dialed manually in an attempt to further identify the carrier. Identification techniques for manual dial-backs are discussed in the following section. The second phone number that was identified (123456891) has the banner “Please press [Enter].” This carrier banner is type of the remote desktop application PCAnywhere. This system can be reidied using the PCAnywhere client. The system identity in the log file shown in Figure 2.11 contains a banner for what appears to be an IDS system. Some IDS systems have dial-up access in case the TCP/IP network goes down for remote management and maintenance. In this case, system information is already disclosed within the carrier banner, and when manually reidied, the system may just identify itself, lowering the level of effort required to potentially compromise the system.

# Figure 2.11 Found Log

```
Found Log.log
C-mon-loc01 01:10:48 1234567895: CONNECT 2400
S=C=
T 23688-B G=B C=T
23688-B
C-mon-loc02 01:10:52 1234567891: CONNECT 2400
-Please press [Enter]...-
C-mon-loc02 01:10:53 1234567892: CONNECT 2400
PROMPT>IDIVER: welcome to the System IDS shell
$
```

NOTE

Not all identified modems have a banner. Systems that are identified in the Found.log that do not have a corresponding banner should be reied manually.