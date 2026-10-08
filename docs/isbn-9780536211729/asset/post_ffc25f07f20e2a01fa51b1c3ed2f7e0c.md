
Most likely, a cracker has violated the Federal Aviation Administration. The Non-authoritative answer simply means that a name server (either MindSpring's or one upstream from it) has cached the IP to name record and this has been used rather than the official top-level name server for .gov.

Supply the value faa.gov to the government's lookup service and you should see

```
Whois Search Results:
[Registration]
Federal Aviation Administration (FAA-DOM)
800 Independence Ave. SW
Washington, DC 20591

[About GSA]
Domain Name: FAA.GOV
Status: ACTIVE
Domain Type: Federal

Technical Contact:
Coronel, Gus X. (GXC)
(202) 267-7828
GUS.CTR.CORONEL@FAA.GOV

Administrative Contact:
Hayes, Alan (AH3)
(202) 267-7357
ALAN.HAYES@FAA.DOT.GOV

Domain servers in listed order:

ENIGMA.FAA.GOV 204.108.10.2
LABYRINTH.FAA.GOV 207.104.92.2
CHASSIS7.TGF.TC.FAA.GOV 155.178.206.153

Record last updated on 12-Apr-99.
```

The technical contact is the one you want to contact.

To trace a U.S. military address use

```
www.nic.mil/
```

Remember that the system probably is compromised, so a phone call or overnight postal letter is much preferred over e-mail because the e-mail may be read by the cracker and deleted. The e-mail would serve only to alert the cracker that you are on to him. It is unusual for a System Administrator to be a cracker.

## 14.6 Using ping

The ping program is useful in determining whether a node is up and on the Internet, such as your cracker's node. This also is useful to see if you were given a bogus IP address. (The IP address could be that of a valid node unrelated to the breach, of course.) You might want to use ping from a different system in a different domain (for example, your home system if you are investigating a problem with your work system). This would reduce the likelihood of “tipping your hand” to the cracker. Of course, if you have references to your home system in your work system, such as in your .rhosts file or in e-mail, this might not help and your home system now may be compromised as well.

The ping program uses ICMP. Most systems respond to it and do not log someone pinging to them. Many firewalls do block it, however, because it is a cracker technique. In this case, use traceroute instead. Both you and your cracker can make use of ping.

> Pings to your systems can be detected and logged with **PingLogger**, available from the CD-ROM and from
>
> ftp://sunsite.org.uk/Mirrors/contrib.redhat.com
> /libc6/SRPMS/pinglogger-1.1-2.src.rpm

There are two particularly creative techniques that you can use ping for. The first is seeing what the round trip time is. This will give you an idea of how far away the cracker is and what types of networks he is using. The round trip times given by ping are used here. (You would need to divide the time that ping gives by two to get the one-way time.)

Times in the 1–10 ms (millisecond) range probably are on your LAN (local area network). Times up to 120 ms are likely somewhere else in the U.S. (assuming that is where you are and you are on a T1). Times typically between 140 and 200 ms are over a PPP connection to somewhere on the same continent.

I see 110 ms ping times to the UK and 130 to 250 ms pings to continental Europe, 250 to 350 ms ping times to Japan, 175 to 400 ms times to Israel, 300 ms and up to New Zealand, and 470 ms or more to Australia. These timings were made on a T1 in Atlanta supplied by UUNet late at night and represent “best case” results.

By using traceroute to note the transit time between the cracker's system and the one next to it, you can determine if she is on a PPP connection, Ethernet, or something in between. If the transit time indicates a PPP connection, she probably is on a home system hosted by an ISP or her company, or she might be using a stolen account.

The second useful thing you can determine is her hours of operation. Most freelance crackers work late at night, both because you are less likely to be on the system noticing them and because they have school or work during the day. If she only logs on during the day, she is using a work account.

Do try to determine what the time zone of her location is and determine when day and night are there. The U.S. West Coast, including California, is three hours behind the East Coast, the British Isles are five hours ahead of the East Coast, and Western Europe is six hours ahead of the U.S. East Coast. The URL `www.cavu.com/sunset.html` may be used to determine the time zone of almost any place on the earth.

## 14.7 Using traceroute

The `traceroute` program is very useful for determining the route to a node, such as your cracker’s. This is useful if it is not obvious what route was used to get to you. It is possible, though unlikely, that the route to your system is different from the route in the opposite direction. By analyzing the few nodes nearest to your cracker’s, you can determine what company, ISP (Internet Service Provider), or agency is being used to connect her to the Internet. By nearest, we mean the one just before it on the traceroute results, the one just before that one, etc. The interpretation of these timings was discussed in “Using `ping`” on page 506.

> The names of intermediate routers often tell their geographic locations. Commonly a router’s name will contain its city or the three-letter identifier of the nearest large airport. These identifiers can be decoded at
>
> `www.cavu.com/sunset.html`

These entities are the ones you will want to contact first to try to shut down the cracker. Realize that some of these systems might be compromised and some even might be under the authority of the cracker. You will want to use the techniques discussed earlier in this section to get phone contacts for these upstream systems. The `traceroute` program has an advantage over `ping` in that many sites now block `ping` requests because it can be used for DoS and other attacks. `Traceroute` packets (usually UDP packets on high port numbers) rarely are blocked.

The `traceroute` program has a variety of flags that can be useful, particularly with misconfigured systems. Usually, only the destination system’s host name or numeric IP address is supplied as an argument. It then lists the data for each “hop,” including the hop number, host name and IP, and the minimum, average, and maximum transit times. The data for each hop is generated when that host responds to a packet that has exceeded its Time To Life (TTL) with an ICMP TIME_EXCEEDED error. Some systems do not generate this message to avoid spending the bandwidth, for confidentiality, or just because they do not have to.

If the cracker is good, she entered your system from someone else's system that she cracked already. Most SysAdmins, even with years of experience, do not have much knowledge and experience in tracking down crackers. Even those that do frequently do not have the time. You might need to help the compromised system's SysAdmin interpret his system logs. If the compromised system belongs to a very large organization, it probably has a group dedicated to computer security issues.

## 14.8 Neighboring Systems' Results

## 14.9 A Recent International Tracking of a Cracker

In 1999, a system behind the firewall of a very large British company was used to steal our sunset database of airport names, cities, and locations in our sunset Web page (by their doing a query on every three-letter combination as an airport ID). I worked from Atlanta. Our Web server was in New Hampshire. The violating IP was traced to a British company with London telephone city codes.

A single polite but firm e-mail to the person listed as the responsible party for that domain got action. We received a number of overseas phone calls and they did an extensive audit of their logs. Their people were very knowledgeable and helpful and a pleasure to deal with. They stated that if they could find the employee responsible he would be sacked!

I provided our detailed logs of the cracking. I compared the system's time to the exact actual time and provided them with the correction. Again, he did not actually "break" security because he just made requests to our Web server. However, he did load down the server to an unreasonable degree, obtained the entire contents of our database, and reduced service levels to legitimate users. It is not clear whether his use actually was illegal, because we did not have a *use policy* on the site. We now do have such a use policy so that exceeding it will be considered unauthorized use.

Unfortunately, there were many, many systems behind this firewall with some not being theirs but rather being those of associated companies. After they scanned logs of systems in half a dozen countries, they did not find any that matched. They did suspect that the culprit was using a system in California belonging to one of their associated companies. Thus, he went from California to London and then back across the Atlantic to New Hampshire. (Because we had some phony airports in the database to detect theft we might catch him yet!)

## 14.10 Be Sure You Found the Attacker

Naturally, you will want to stop the attacker from causing further harm to your systems and anyone else's. You probably want him punished as well and you might want to hand him a bill for your costs in finding and repairing the damage. You probably have the IP address of the system used to violate yours. Without this or similar identifying information, you probably do not have any clues as to who attacked you.
