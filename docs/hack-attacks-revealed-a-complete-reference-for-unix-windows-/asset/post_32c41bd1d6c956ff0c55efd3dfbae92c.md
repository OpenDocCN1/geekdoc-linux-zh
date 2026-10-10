
![](img/ba85bb40c695c02adae8cbd6666f2e0c_432_0.png)

...aid of his site), and I always made sure I “had root” if I were going to modify anything. I always made sure the logs were wiped clean of my presence; and when I was certain I couldn’t be caught, I informed the system administrator of the security hole that I used to get in through.

I know that four years is not a very long time, but in my four years, I’ve seen a lot change. Yes, there are still newbies, those who want to learn, but are possibly on the wrong track; maybe they’re using tools like Back Orifice—just as many used e-mail bombers when I was new to the scene. Groups like milw/orm seem to be made up of a bunch of immature kids who are having fun with the exploits they found at rootshell.com, and are making idiots of themselves to the real hacking community.

Nobody is perfect, but it seems that many of today’s newbies are headed down a path to nowhere. Hacking is not about defacing a Web page, nor about making a name for yourself. Hacking is about many different things: learning about new operating systems, learning programming languages, learning as much as you can about as many things as you can. [To do that you have to] immerse yourself in a pool of technical data, get some good books; install Linux or *BSD. Learn; learn everything you can. Life is short; don’t waste your time fighting petty little wars and searching for fame. As someone who’s had a Web site with over a quarter-million hits, I can tell you, fame isn’t all it’s cracked up to be.

Go out and do what makes you happy. Don’t worry about what anybody thinks. Go create something that will be useful for people; don’t destroy the hard work of others. If you find a security hole in a server, notify the system administrator, and point them in the direction of how to fix the hole. It’s much more rewarding to help people than it is to destroy their work.

In closing, I hope this article has helped to open the eyes of people who are defacing Web sites. I hope you think about what I’ve said, and take it to heart. The craze over hacking Web pages has gone on far too long. Too much work has been destroyed. How would you feel if it were your hard work that was destroyed?

The initial goal of any hacker when targeting a Web page hack is to steal passwords. If a hacker cannot successfully install a remote-control daemon to gain access to modify Web pages, he or she will typically attempt to obtain login passwords using one of the following methods:

- FTP hacking
- Telnet hacking
- Password-stealing Trojans
- Social engineering (swindling)
- Breach of HTTP administration front ends.
- Exploitation of Web-authoring service daemons, such as MS FrontPage
- Anonymous FTP login and password file search (e.g., /etc folder)
- Search of popular Internet spiders for published exploitable pwd files

The following scenario of an actual successful Web page hack should help to clarify the material in this section. For the purposes of this discussion, the hack has been broken into five simple steps.

> The target company in this real-world scenario signed an agreement waiver as part of the requirements for a Web site integrity security assessment.

# Step 1: Conduct a Little Research

The purpose of this step is to obtain some target discovery information. The hacking analysis begins with only a company name, in this case, WebHackVictim, Inc. As described previously, this step entails locating the target company’s network domain name on the Internet. Again, the domain name is the address of a device connected to the Internet or any other TCP/IP network in a system that uses words to identify servers, organizations, and types of organizations, in this form: www.companyname.com.

As noted earlier, finding a specific network on the Internet can be like finding the proverbial needle in a haystack: it’s difficult, but possible. As you know by now, Whois is an Internet service that enables a user to find information, such as a URL for a given company or a user who has an account at that domain.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_433_0.png)

**Figure 8.22** Whois verification example.

Now that the target company has been located as a valid Internet domain, the next part of this step is to click on the domain link within the Whois search result to verify the target company. Address verification will substantiate the correct target company URL; in short, it is confirmation of success.

# Step 2: Detail Discovery Information

The purpose of this step is to obtain more detailed target discovery information before beginning the attack attempt. This involves executing a simple host ICMP echo request (PING) to reveal the IP address for www.webhackvictim.com. PING can be executed from an MS-DOS window (in Microsoft Windows) or a Terminal Console Session (in UNIX). In a nutshell, the process by which the PING command reveals the IP address can be broken down into five steps:

1. A station executes a PING request.
2. The request queries your own DNS or your ISP's registered DNS for name resolution.
3. The URL—for example www.zyxinc.com—is foreign to your network, so the query is sent to an InterNIC DNS.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_434_0.png)

**Figure 8.23** Domain name resolution process.

4. From the InterNIC DNS, the domain zyxinc.com is matched with an IP address of XYZ's own DNS or ISP DNS (207.237.2.2), using the same discovery techniques from Chapter 5 and forwarded.
5. XYZ Inc.'s ISP, hosting the DNS services, matches and resolves the domain www.zyxinc.com to an IP address, and forwards the packet to XYZ's Web server, ultimately returning with a response (see Figure 8.23).

The target domain IP address is revealed with an ICMP echo (PING) request in Figure 8.24.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_435_0.png)

**Figure 8.24** ICMP echo request.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_435_1.png)

**Figure 8.25** Extended ping query.

Standard DNS entries for domains usually include name-to-IP address records for WWW (Internet Web Server), FTP (FTP Server), and so on. Extended PING queries may reveal these hosts on our target network 207.155.248.0 as shown in Figure 8.25.

Unfortunately, in this case, the target either doesn't maintain a standard DNS entry pool or the FTP service is bound by a different name-to-IP address, so we'll have to perform a standard IP port scan to unveil any potential vulnerable services. Normally, we would only scan to discover active addresses and their open ports on the entire network (remember, hackers would not spend a lot of time scanning with penetration and vulnerability testing, as that could lead to their own detection). A standard target site scan would begin with the assumption that the network is a full Class C (refer to Chapter 1). With these parameters, we would set the scanner for an address range of 207.155.248.1 through 207.155.248.254, and 24 bits in the mask, or 255.255.255.0, to accommodate our earlier DNS discovery findings:

www www.webhackvictim.com 207.155.248.7

However, at this time, we're interested in only the Web server at 207.155.248.7, so let's get right down to it and run the scan with the time-out set to 2 seconds. This should be enough time to discover open ports on this system:

```
207.155.248.7: 11, 15, 19, 21, 23, 25, 80
```

Bingo! We hit the jackpot! Note the following:

- **Port 11: Sysstat.** The sysstat service is a UNIX server function that provides the capability to remotely list running processes. From this information, a hacker can pick and choose which attacks are most successful.
- **Port 15: Netstat.** The netstat command allows the display of the status of active network connections, MTU size, and so on. From this information, a hacker can make a hypothesis about trust relationships to infiltrate outside the current domain.
- **Port 19: Chargen.** The chargen service is designed to generate a stream of characters for testing purposes. Remote attackers can abuse this service by forming a loop from the system's echo service with the chargen service. The attacker does not need to be on the current subnet to cause heavy network degradation with this spoofed network session.
