# **14.6 Using ping**

The ping program is useful in determining whether a node is up and on the Internet, such as your cracker's node. This also is useful to see if you were given a bogus IP address. (The IP address could be that of a valid node unrelated to the breach, of course.) You might want to use ping from a different system in a different domain (for example, your home system if you are investigating a problem with your work system). This would reduce the likelihood of “tipping your hand” to the cracker. Of course, if you have references to your home system in your work system, such as in your .rhosts file or in e-mail, this might not help and your home system now may be compromised as well.

The ping program uses ICMP. Most systems respond to it and do not log someone pinging to them. Many firewalls do block it, however, because it is a cracker technique. In this case, use traceroute instead. Both you and your cracker can make use of ping.

> Pings to your systems can be detected and logged with **PingLogger**, available from the CD-ROM and from 

> ftp://sunsite.org.uk/Mirrors/contrib.redhat.com 
> /libc6/SRPMS/pinglogger-1.1-2.src.rpm

There are two particularly creative techniques that you can use ping for. The first is seeing what the round trip time is. This will give you an idea of how far away the cracker is and what types of networks he is using. The round trip times given by ping are used here. (You would need to divide the time that ping gives by two to get the one-way time.)

Times in the 1–10 ms (millisecond) range probably are on your LAN (local area network). Times up to 120 ms are likely somewhere else in the U.S. (assuming that is where you are and you are on a T1). Times typically between 140 and 200 ms are over a PPP connection to somewhere on the same continent.

I see 110 ms ping times to the UK and 130 to 250 ms pings to continental Europe, 250 to 350 ms ping times to Japan, 175 to 400 ms times to Israel, 300 ms and up to New Zealand, and 470 ms or more to Australia. These timings were made on a T1 in Atlanta supplied by UUNet late at night and represent “best case” results.

By using traceroute to note the transit time between the cracker's system and the one next to it, you can determine if she is on a PPP connection, Ethernet, or something in between. If the transit time indicates a PPP connection, she probably is on a home system hosted by an ISP or her company, or she might be using a stolen account.

The second useful thing you can determine is her hours of operation. Most freelance crackers work late at night, both because you are less likely to be on the system noticing them and because they have school or work during the day. If she only logs on during the day, she is using a work account.

Do try to determine what the time zone of her location is and determine when day and night are there. The U.S. West Coast, including California, is three hours behind the East