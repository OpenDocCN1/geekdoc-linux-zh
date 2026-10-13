
;; 153.77.37.208.IN-ADDR.ARPA, type = PTR, class = IN
153.77.37.208.IN-ADDR.ARPA. 2H IN PTR w153.z200837077.nyc-ny.dsl.cnc.net.
77.37.208.IN-ADDR.ARPA. 2H IN NS nameserver3.concentric.net.
77.37.208.IN-ADDR.ARPA. 2H IN NS nameserver1.concentric.net.
77.37.208.IN-ADDR.ARPA. 2H IN NS nameserver2.concentric.net.
rcode = 0 (Success), ancount=1

The following answer is not authoritative:
The following answer is not verified as authentic by the server:
153.77.37.208.IN-ADDR.ARPA 7200 IN PTR w153.z200837077.nyc-ny.dsl.cnc.net
For authoritative answers, see:
77.37.208.IN-ADDR.ARPA 7200 IN NS nameserver3.concentric.net
77.37.208.IN-ADDR.ARPA 7200 IN NS nameserver1.concentric.net
77.37.208.IN-ADDR.ARPA 7200 IN NS nameserver2.concentric.net

The resolved name is buried in the middle of this information:
w153.z200837077.nyc-ny.dsl.cnc.net.

- 2. The next step is to look up the complete domain registration record:

```
# whois -r cnc.net
[whois.crsnic.net]

Whois Server Version 1.3

Domain names in the .com, .net, and .org domains can now be registered
with many different competing registrars. Go to http://www.internic.net
for detailed information.

Domain Name: CNC.NET
Registrar: NETWORK SOLUTIONS, INC.
Whois Server: whois.networksolutions.com
Referral URL: http://www.networksolutions.com
Name Server: NAMESERVER3.CONCENTRIC.NET
Name Server: NAMESERVER1.CONCENTRIC.NET
Name Server: NAMESERVER2.CONCENTRIC.NET
Updated Date: 05-nov-2001

>>> Last update of whois database: Tue, 19 Mar 2002 05:21:50 EST <<<

[whois.networksolutions.com]

Registrant:
Concentric Network Corporation (CNC6-DOM)
1400 Parkmoor Avenue
San Jose, CA 95126-3429

Domain Name: CNC.NET
```

Administrative Contact:
Schairer, David R (DRS9) nja1@CONCENTRIC.NET
Concentric Network Corp.
1400 Parkmoor Ave
Cupertino, CA 95014
(408) 817-2800 (800) 745-2747 ext. 2800 (FAX) (408) 817-2630
Technical Contact:
DNS & IP ADMIN (DIA-ORG) hostmaster@CONCENTRIC.NET
Concentric Network Corporation
1400 Parkmoor Avenue
San Jose, CA 95126-3429
(408) 817-2800
Fax: (408) 817-2630
Billing Contact:
XO Communications, Hostmaster (CNCXCH-ORG) hostmaster@XOHOST.COM
XO Communications
1400 Parkmoor Ave
San Jose, CA 95126
408-817-2800
Fax: 408-817-2810

Record last updated on 02-Mar-2001.
Record expires on 06-Mar-2004.
Record created on 05-Mar-1997.
Database last updated on 18-Mar-2002 22:31:00 EST.

Domain servers in listed order:
NAMESERVER3.CONCENTRIC.NET 206.173.119.72
NAMESERVER2.CONCENTRIC.NET 207.155.184.72

Concentric Networks is a large ISP based in Northern California.

3. We'll send them an e-mail message, but, alas, I don't expect any sort of meaningful response:

```
# mail -s "One of your customers was trying to hack into my system"
abuse@cnc.net
Hello. I have tracked backward and found that one of the computers in your domain (w153.z208037077.nyc-ny.dsl.cnc.net) was trying to hack into my Linux server. In the "/var/log/secure" log file, I find the following message from 'sshd':
Mar 10 10:22:14 staging sshd[12114]: Did not receive identification string
from 208.37.77.153.
```

A reverse lookup of that IP address returns:
153.77.37.208.in-addr.arpa. domain name pointer w153.z208037077.nyc-ny.dsl.cnc.net.

> Can you please work backward in your usage logs to ascertain what computer has the specified IP address of 208.37.77.153, and identify the culprit?
> Needless to say, I don't want people port-scanning my server!
> 
> Thanks for your assistance on this matter.
> 
> Dave Taylor
> taylor@intuitive.com

4. About 15 minutes later, we receive the following:

The original message was received at Tue, 19 Mar 2002 13:46:52 -0500 (EST)

```
.... The following addresses had permanent fatal errors ....
(expanded from: <abuse@cncx.net>)

.... Transcript of session follows ....
550 abuse@cncx.net... Host unknown (Name server: cncx.net: host not found)
```

Oh well, at least we can see how to work backward in our log files, and at least we tried...

It's not uncommon to find people trying to probe your ports: Indeed, it's a matter of five minutes of shell programming to write a "port scanner" that will pick an IP address, then see what Internet services, if any, are listening. Once that's ascertained, there are tools available to try and break in using a specific service "exploit."

If it sounds a bit depressing, it should. The best thing you can do for security is to ensure that your system is properly configured, that you keep an eye on your log files, that you have a properly configured firewall, and that you have reliable backups just in case.

There are also some very good books about Unix security, three of which I'll highlight here:

- *Hacking Linux Exposed* by Brian Hatch et al. (McGraw-Hill) has a good explanation of what hackers do to try and gain entry into your system, though at the expense of less coverage of how to avoid the problem in the first place.
- *Practical Unix and Internet Security* by Simson Garfinkel and Gene Spafford (O'Reilly) is more academic, but a definitive reference on this topic.
- *Maximum Linux Security* by Anonymous (Sams) is another option. A quick search on Amazon or Barnes & Noble will reveal quite a few other choices if none of these jump out at you.

We'll return to the topic of security again in the last hour.

## The httpd Log File

There’s another log file that is well worth exploring in some detail, as it’s often the main purpose for a Unix server in the first place: the Web server log.

There are different Web servers available, but by far the most popular is Apache, a freely distributed HTTP daemon that offers remarkable flexibility, power, and configurability. It is included on just about every modern Unix distribution, and you can download the Apache distribution at www.apache.org.

## Task 16.3: Exploring the httpd Log File

The last log file we’ll examine in this hour is the Apache Web server log file, actually a set of files all stored in /var/log/httpd.

- 1. Here’s what’s typically in that directory:

```
# cd /var/log/httpd
# ls -s
total 984
35 access_log   3 error_log   1 ssl_engine_log   0 ssl_request_log
252 access_log.1   3 error_log.1   0 ssl_mutex.19348   0 ssl_scache.sem
217 access_log.2   44 error_log.2   0 ssl_mutex.4766
141 access_log.3   27 error_log.3   0 ssl_mutex.827
188 access_log.4   44 error_log.4   0 ssl_mutex.641
```

To make things more interesting, however, we’ll analyze the log files from a busier Web server with larger log files:

```
# ls -s
total 4200
2594 access_log   654 agent_log   33 error_log   919 referer_log
```

- 2. The first snippet of information you would like to extract from your log files is a count of hits, which proves remarkably easy to do:

```
# wc -l access_log
12384 access_log
```

12,384 hits, but in what period of time? Again, just look at the first and last lines of the log file to find out:

This represents all usage between midnight and 6:05 p.m., a total of 18 hours. This means that this server is seeing a respectable, but not overwhelming, 688 (12384-18) hits per hour, or 11.4 (688÷60) hits per minute.

- 3. To extract more information from this log file, a quick summary of the log file format is required. I won't explain everything in this hour (we'll look at Apache in more detail later in the book), but here's the essential field layout:

```
visitor-domain . date&time timezone operation URL - return-code
►bytes-sent ...
```

With this information, we can quickly extract interesting information, like what domains account for the greatest number of hits:

```
# awk '{print $1}' access_log | sort | uniq -c | sort -rn | head -10
305 193.190.216.249
208 pc03.wimpb.zgora.pl
175 164.156.231.55
145 204.185.56.252
117 216.35.169.126
110 slb-proxy-03.boeing.com
84 194.131.98.235
78 216-203.142-177.customer.algx.net
75 61.11.78.180
70 209.248.92.29
```

Again, the host command can do a reverse lookup for the topmost domain:

```
# host -dv 193.190.216.249 | grep "IN SOA"
216.190.193.IN-ADDR.ARPA. 2h59m40s IN SOA www.senate.be. sysadmin.senate.be.
```

A computer in the Belgian Senate accounts for more traffic than any other system visiting the Web site in this 18 hour window. Surprised?

```
# host -dv 164.156.231.55 | grep "IN SOA"
156.164.156.IN-ADDR.ARPA. 3H IN SOA jasper.cmic.state.pa.us. security.state.pa.us
```

IP address number three is the Pennsylvanian office of Social Security!

- 4. Another common query to the Apache log file is about what URLs are most commonly requested. This is easy to calculate when you notice that field seven is the requested URL:

```
# awk '{print $7}' access_log | sort | uniq -c | sort -rn | head
1334 /cgi-local/etymologic.cgi
699 /cgi-local/trivial.cgi
508 /
437 /Taylor/Graphics/biohazard.gif
219 /sites/trivial/Graphics/kudos.gif
217 /sites/trivial/Graphics/intsys.gif
213 /sites/etymologic/Graphics/bottom-bar.gif
212 /sites/etymologic/Graphics/top-bar.gif
204 /sites/etymologic/Graphics/bonus-com.gif
203 /sites/etymologic/Graphics/linkbw2.gif
```
