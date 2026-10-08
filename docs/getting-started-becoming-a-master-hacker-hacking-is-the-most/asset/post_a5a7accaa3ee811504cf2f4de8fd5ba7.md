
## DNS Information Gathering Techniques

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_175_0.png)

`kali> dig microsoft.com ns`

Where `ns` indicates that we are looking for the nameserver.

As you can see in the screenshot above, we were able to pull the nameserver records for microsoft.com.

If we want the mail server records for microsoft.com, we can query the DNS server with:

`kali> dig microsoft.com mx`

Where `mx` indicates that we are looking for the mail server records.

```bash
root@kali-2019:~# dig @75.75.75.75 microsoft.com axfr
; <<>> DiG 9.11.5-P1-1-Debian <<>> @75.75.75.75 microsoft.com axfr
; (1 server found)
;; Global options: +cmd
; Transfer failed.
```

## Enumerating Subdomains

`root@kali-2019:~# dnsenum`

```text
Smartmatch is experimental at /usr/bin/dnsenum line 698.
Smartmatch is experimental at /usr/bin/dnsenum line 698.
dnsenum VERSION:1.2.4
Usage: dnsenum [Options] <domain>
[Options]:
Note: the brute force -f switch is obligatory.
GENERAL OPTIONS:
  --dnsserver <server>
                  Use this DNS server for A, NS and MX queries.
    --enum        Shortcut option equivalent to --threads 5 -s 15 -w.
    -h, --help    Print this help message.
    --noreverse   Skip the reverse lookup operations.
    --nocolor     Disable ANSI Color output.
    --private     Show and save private ips at the end of the file domain_ips.txt.
    --subfile <file> Write all valid subdomains to this file.
    -t, --timeout <value>
                  The tcp and udp timeout values in seconds (default: 10s).
    --threads <value>
                  The number of threads that will perform different queries.
    -v, --verbose Be verbose: show all the progress and all the error messages.
GOOGLE SCRAPING OPTIONS:
    -p, --pages <value>
                  The number of google search pages to process when scraping names,
                  the default is 5 pages, the -s switch must be specified.
    -s, --scrap <value>
                  The maximum number of subdomains that will be scraped from Google (default 15).
BRUTE FORCE OPTIONS:
    -f, --file <file>
                  Read subdomains from this file to perform brute force.
```

As you can see in the screenshot above, we successfully pulled the mail server records for microsoft.com. Finally, we can attempt to do a zone transfer (in DNS terminology, a zone transfer is an update to DNS records) on microsoft.com by entering:

`kali> dig @75.75.75.75 microsoft.com axfr`

Where `@75.75.75.75` is the IP address of the DNS server, and `axfr` is the command for a zone transfer.

Note that zone transfers are malicious and only possible on improperly configured DNS servers. In our case here, the DNS server would not allow us to do a zone transfer.

## Bruteforcing Subdomains using dnsenum.pl

Within Kali, we have several DNS information gathering tools. `dnsenum` is a Perl script and an excellent tool for automating the extraction of all the DNS information we have been extracting above manually and more.

Open a terminal and enter `dnsenum` at the prompt.

Note that dnsenum’s syntax is relatively simple:

`dnsenum.pl [Options] <domain>`

In our case, we are using dnsenum to attempt a dictionary attack on the subdomains of kali.org with the DNS file supplied by the script developers (you can use your own if you like). To do this, we need to use the `-f` switch and the absolute path to our list of potential subdomain names (`/usr/share/dnsenum/dns.txt`) and then the domain we want to search for subdomains.

```bash
root@kali-2019:~# dnsenum -f /usr/share/dnsenum/dns.txt kali.org
Smartmatch is experimental at /usr/bin/dnsenum line 698.
Smartmatch is experimental at /usr/bin/dnsenum line 698.
dnsenum VERSION:1.2.4

------ kali.org ------

Host's addresses:

kali.org.                  60    IN   A   192.124.249.10

Name Servers:

ns1.no-ip.com.             11842  IN   A   194.62.181.53
ns3.no-ip.com.              10611  IN   A   204.16.255.53
ns4.no-ip.com.              10973  IN   A   204.16.254.53
ns5.no-ip.com.              17082  IN   A   194.62.181.53
ns5.no-ip.com.              12491  IN   A   194.62.180.53

Mail (MX) Servers:

alt1.aspmx.l.google.com.     108  IN   A   209.85.144.27
alt3.aspmx.l.google.com.     107  IN   A   64.233.100.26
alt2.aspmx.l.google.com.     107  IN   A   74.125.141.26
aspmx.l.google.com.          205  IN   A   172.217.214.26
alt4.aspmx.l.google.com.     293  IN   A   74.125.193.26

archive.kali.org.       60      IN      CNAME   hera.kali.org.
hera.kali.org.         60      IN      A       192.99.45.148
backup.kali.org.       60      IN      CNAME   polyhymnia.kali.org.
polyhymnia.kali.org.   60      IN      A       54.39.103.103
bugs.kali.org.         60      IN      A       192.124.249.169
forums.kali.org.       60      IN      A       192.124.249.12
http.kali.org.         60      IN      CNAME   hebe.kali.org.
hebe.kali.org.         60      IN      A       192.99.200.113
mail.kali.org.         60      IN      CNAME   apollo.kali.org.
apollo.kali.org.       60      IN      A       23.239.31.92
old.kali.org.          60      IN      CNAME   tersiphore.kali.org.
tersiphore.kali.org.   60      IN      A       54.39.49.227
pan.kali.org.          60      IN      A       167.114.101.148
www.kali.org.          60      IN      A       192.124.249.10

kali.org class C netranges:

23.239.31.0/24
54.39.49.0/24
54.39.103.0/24
167.114.101.0/24
192.99.45.0/24
192.99.200.0/24
192.124.249.0/24
```

In this case, let’s use www.kali.org. We would write our command like this below:

`kali> dnsenum.pl -f /usr/share/dnsenum/dns.txt kali.org`

As you can see below, once we hit Enter, dnsenum begins by enumerating the nameservers and mail servers for www.kali.org. It then tries to brute force subdomains using the list of potential subdomains we provided and the Class C netranges. Finally, it attempts a zone transfer unsuccessfully.

```text
**Name Servers:**

ns1.hastydns.com. 11 IN A 66.135.47.136

**Mail (MX) Servers:**

**Trying Zone Transfers and getting Bind Versions:**

Trying Zone Transfer for hakin9.com on ns2.hastydns.com...
AXFR record query failed: connection failed

Trying Zone Transfer for hakin9.com on ns1.hastydns.com ...
AXFR record query failed: connection failed
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_179_0.png)

## Querying the Target’s DNS Cache to Determine its Antivirus Software

Now that we understand a bit about how we can cultivate DNS service for information, let’s look at another more sophisticated use of DNS for providing information on the target.

I’ve included this technique not because of its practicality, but for its ingenuity and creativity—two essential attributes of a master hacker.

As a hacker, it is often critical to know what antivirus software the target is running. Unless you have created or bought a zero-day exploit, it will likely be detected and quarantined by the antivirus software. As a result, your days, weeks, or months of work will be lost.

Not all antivirus software is the same! Some are good, and some are bad. Some detect certain malware, and some detect others. As a result, an attack may work against one antivirus and not against another. If we can know ahead of time what antivirus the target is using, we can tailor an attack that evades that software.

When firms have their own DNS server, that server caches every DNS query from every employee. If we can examine the DNS cache, we can see every domain that has been queried. This means if we can examine the DNS cache, we can determine which AV software domain (Symantec, McAfee, Kaspersky, etc.) has been queried and which has not. The target company will be using one or all of the AV domains in the list. We don't know which, but we do know that AV companies not on the list are NOT being used.

That information alone can help us determine which attack works.

As this is more of an intermediate-to-advanced reconnaissance technique, I will simply leave you with a link where you can learn more: [https://www.hackers-arise.com/single-post/2016/05/23/How-to-Use-Recon-to-Determine-the-Target-s-AV-Software-1]
