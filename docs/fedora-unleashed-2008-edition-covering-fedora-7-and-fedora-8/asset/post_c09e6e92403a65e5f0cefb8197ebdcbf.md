
little choice but to try and tell your ISP what to do to fix the problem. If the ISP staff refuses to listen, find a new ISP (or live with broken DNS).

Another typical symptom of failing reverse lookups is an abnormally long delay on connection attempts. This happens when the server's query for a PTR record is not answered and times out (often because of network problems or the nameserver being down). This can be baffling to diagnose, but you should suspect DNS problems whenever you hear questions such as "Hey! Why is my web browser taking so long to connect?"

## Maintaining Accurate Serial Numbers

Accurate serial numbers are very important to the correct operation of slave servers. An increase in the serial number of a zone causes slaves to reload the zone and update their local caches.

A common mistake that system administrators make is forgetting to increment the serial number after a change to the zone data. If you make this mistake, secondary nameservers don't reload the zone, and continue to serve old data. If you suspect that the data on the master and slave servers is out of sync, you can use `dig` to view the `SOA` record for the zone on each server (`dig @master domain SOA` and `dig @slave domain SOA`) and compare the serial numbers in the responses.

Another common problem is setting the serial number to an incorrect value—either too small or too large. A too-small serial number causes slaves to think that they possess a more up-to-date copy of the zone data, but this is easily corrected by increasing the serial number as necessary. A too-large serial number is more problematic and requires more elaborate measures to repair.

Serial number comparisons are defined in such a way that if a serial number—when subtracted from another with no overflow correction—results in a positive number, the second number is newer than the first, and a zone transfer is required. (See RFC 1982, "Serial Number Arithmetic," for details.) You can exploit this property by temporarily setting the serial number to 2^31 (4,294,967,296), waiting for all the slaves to reload the zone, and then setting it to the correct number.

## Troubleshooting Problems in Zone Files

The most common error in zone data is forgetting that names in a zone file are relative to the origin of the zone, not to the root. Writing `www.example.com` in the zone file for `example.com` and expecting it to be fully qualified causes names such as `www.example.com.example.com` to show up in the DNS. You should either write `www`, which is qualified to the correct `www.example.com`, or write `www.example.com.` (with the trailing period) to indicate that the name is fully qualified.

The `SOA` record should contain (as the first field) the domain name of the master server (not a `CNAME`) and a contact address (with the `@` replaced by a `.`) to report problems to.

Mail sent to this address should be read frequently. The other fields should contain sensible values for your zone, and the serial number should be correctly incremented after each change.

As discussed earlier, A and PTR records should always match; that is, the A record pointed to by a PTR record should point back to the address of the PTR record. Remember to quote the two arguments of HINFO records if they contain any whitespace. Avoid the use of CNAME records for MX, NS, and SOA records.

In general, after making changes to zone data, it is a good idea to reload named and examine the logs for any errors that cause named to complain or reject the zone. Even better, you could use one of the verification tools, such as *dnswalk*, discussed briefly next.

### Tools for Troubleshooting

BIND includes the always useful *dig* program, as well as *named-checkconf* (to check /etc/named.conf for syntax errors) and *named-checkzone* (to do the same for zone files). We also especially recommend *dnswalk* and *nslint*. *dnswalk* is a Perl script that scans the DNS setup of a given domain for problems. It should be used in conjunction with RFC 1912, which explains most of the problems it detects. *nslint*, like the analogous *lint* utility for C programs, searches for common BIND and zone file configuration errors.

By occasionally using these programs to troubleshoot DNS problems (especially after nontrivial zone changes), you go far toward keeping your DNS configuration healthy and trouble free.

### Using Fedora’s BIND Configuration Tool

Fedora provides a dozen or more different graphical configuration tools system administrators can use to configure network (and system) services. One of these tools is system-config-bind, a deceptively simple BIND configuration tool that requires an active X session and must be run with root privileges.

You can launch this client by using the command system-config-bind from a terminal window or by selecting the Domain Name Service menu item from the Server Settings menu. system-config-bind is automatically installed if you select the Fedora configuration tools.

> **NOTE**  
> Using system-config-bind and then saving any changes overwrites existing settings! If you prefer to manually edit your named configuration files, do not use system-config-bind. Always make a backup of the configuration files in any event—you’ll be glad you did.

After you type the root password and press the Enter key, the client launches. You then see its main window, as shown in Figure 23.2.

![](img/34e72348d53ca54c2a1d9c871316691b_571_0.png)

FIGURE 23.2 Fedora's system-config-bind utility can be used to create, modify, and save basic domain nameserver settings.

system-config-bind can be used to add a forward master zone, reverse master zone, MX records, or slave zone. Click the New button to select an entry for configuration, as shown in Figure 23.3.

![](img/34e72348d53ca54c2a1d9c871316691b_571_1.png)

FIGURE 23.3 Use system-config-bind to add a new DNS record to your server or edit the existing settings.

You can edit or delete existing settings by first selecting and then clicking the **Properties** or **Delete** button in the `system-config-bind` dialog. When you finish entering or editing your custom settings, select the Save menu item from the File menu. Configuration files are saved in `/etc/named.conf` and under the `/var/named` directory.

### Managing DNS Security

Security considerations are of vital importance to DNS administrators because DNS was not originally designed to be a secure protocol and a number of successful attacks against BIND have been found over the years. The most important defense is to keep abreast of developments in security circles and act on them promptly.

DNS is especially vulnerable to attacks known as **poisoning** and **spoofing**. *Poisoning* refers to placing incorrect data into the DNS database, which then spreads to clients and caches across the world, potentially causing hundreds of thousands of people to unwittingly use the bad data. Although DNS poisoning can occur because of carelessness, it has serious implications when performed deliberately. What if someone set up a clone of a common website, redirected users to it by DNS poisoning, and then asked them for their credit card numbers? *Spoofing*, the practice of forging network packets and making nameservers believe that they are receiving a valid answer to a query, is one of the ways malicious poisoning can be performed.

BIND has often been criticized as being very insecure, and although recent versions are greatly improved in this regard, DNS administrators today must take several precautions to ensure that its use is adequately protected from attacks. Of course, it is important to always run the latest recommended version of BIND.

> **TIP**
> 
> One of your strongest defenses against DNS security risks is to keep abreast of developments in security circles and act on them promptly. The BugTraQ mailing list, hosted at [http://www.securityfocus.com/](http://www.securityfocus.com/), and the SANS Institute, at [http://www.sans.org/](http://www.sans.org/), are good places to start.

### UNIX Security Considerations

The most important step in securing any UNIX system is to configure the environment BIND in which runs to use all the security mechanisms available to it through the operating system to its advantage. In short, this means that you should apply general security measures to your computer.

Run `named` with as few privileges as it needs to function. Do not run `named` as `root`. Even if an attacker manages to exploit a security hole in BIND, the effects of the break-in can be minimized if `named` is running as user nobody rather than as root. Of course, `named` has to be started as root because it needs to bind to port 53, but it can be instructed to switch to a given user and group with the `-u` and `-g` command-line options.
