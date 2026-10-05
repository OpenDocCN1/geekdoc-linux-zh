
# DNSSEC tools

defined in the zone file. For the sake of illustration, let's assume that the TTL is one day and that keys don't expire for another week. The steps involved are then

- Generate a new ZSK.
- Include it in the zone file.
- Sign or re-sign the zone with the KSK and the old ZSK.
- Signal the name server to reload the zone; the new key is now there.
- Wait 24 hours (the TTL); now everyone has both the old and new keys.
- Sign the zone again with the KSK and the new ZSK.
- Signal the name server to reload the zone.
- Wait 24 hours; now everyone has the new signed zone.
- Remove the old ZSK at your leisure, e.g., the next time the zone changes.

This scheme is called prepublishing. Needless to say, you must start the process at least two TTLs before the point where you need to have everyone using the new key. The waiting periods guarantee that any site with cached values always has a cached key that corresponds to the cached data.

Another variable that affects this process is the time it takes for your slowest server to update its copy of your zone when notified by the master server. So don't wait until the last minute to start your rollover process or re-sign zones whose signatures are expiring. Expired signatures do not validate, so sites that verify DNSSEC signatures will not be able to DNS lookups for your domain.

The mechanism to roll over a KSK is called double signing and its is also pretty straightforward. However, you will need to communicate your new DNS record to your parent or communicate a DLV record to your surrogate parent. Make sure you have positive acknowledgement of the parent or trust anchor repository before you switch to the new KSK. Here are the steps:

- Create a new KSK.
- Include it in the zone file.
- Sign the zone with both old and new KSKs and the ZSK.
- Signal the name server to reload the zone.
- Wait 24 hours (the TTL); now everyone has the new key.
- Notify anyone with a trust anchor for the new KSK record from the zone.
- After confirmation, delete the old KSK record from the zone.
- Re-sign the zone with the new KSK and ZSK.

# DNSSEC tools

Four tools for dealing with DNSSEC deployment and testing in addition to those that come with the BIND and NSD/Unbound distributions: Idns, Sparta, RIPE, and Vages. At least two sets are under development: OpenDNS (opendsec.org) and DNSSHIM. OpenDNS hopes to manage all the mess and complexity that comes with DNSSEC automatically, which sounds wonderful. DNSSHIM is an authoritative DNS server implementation with automatic configuration of slaves and DNSSEC written in Java and Python.

# Chapter 17 DNS: The Domain Name System

ldns tools, lnnetlabs.nl/projects/ldns

ldns, the folks at LNet Labs, is a library of routines for writing DNS tools and a set of example programs that use the library. We list the tools below with a brief statement of what each one does. The tools are all in examples directory except for drill, which has its own directory in the distribution. Man pages can be found with the commands. The top-level README gives brief installation instructions.

- ldns-keygen generates TSIG keys and DNSSEC keys.
- ldns-signzone signs a zone file with either NSEC or NSEC3.
- ldns-verify-zone makes sure RSIG, NSEC, and NSEC3 records are OK.
- ldns-key2ds converts a DNSKEY record to a DS record.
- ldns-rrsig prints out human-readable expiration dates from RSIGs.
- ldns-nsec3-hash prints the N3 hash for a name.
- ldns-revoke sets the revoke flag on a DNSKEY key RR (RFC55011).
- ldns-chaos shows the name server ID info stored in the CHAOS class.
- ldns-keyfetcher fetches DNSSEC keys for zones.
- ldns-read-zone reads a zone and prints it out in various formats.
- ldns-update sends a dynamic update packet.
- ldns-walk walks through a zone, using the DNSSEC records.
- ldns-zplit splits a zone into chunks so it can be signed in parallel.
- ldns-ream recreates zone files with ldns-split.
- ldns-compare-zones shows the differences between two zone files.
- ldns-notify makes a zone's slave servers check for updates.
- ldns-mpa analyzes DNS packets in tcpdump trace files.

Many of these tools are very simple and do only one DNS zone. They were written as examples of using the ldns library and demonstrate how simple the code becomes when the library does all the hard bits for you.

Sparta tools, dnssec-tools.org

The Sparta tool builds on the BIND tools for DNSSEC and includes the following commands:

- zonesigner generates keys and signs zones.
- donuts analyzes zone files and finds errors and inconsistencies.
- donutsd runs donuts at intervals and warns of problems.
- roller, rolldict, and rolint automate key rollovers with the prepublishing scheme for ZSKs and the double signature method for KSKs. See page 662 for the details of these schemes.
- trustman manages trust anchors and includes an implementation of RFC5011 key rollover.
- dnspkt traces the flow of DNS packets during a query/response sequence captured by tcpdump and produces a cool diagram.
- mapper maps your zone files, showing secure and insecure portions.
- validate is a command-line signature validation tool.

# Debugging DNSSEC 665

The web site contains good documentation and tutorials for all of these tools. The source code is available for download and is covered by the BSD license.
Spart maintains DNSSEC libraries written in Perl that are distributed through CPAN. It also distributes patches to several software packages (including Firefox, Thunderbird, Postfix, sendmail, libSPF, and OpenSSH) to make them more DNSSEC aware.

RIPE tools, ripe.net

RIPE's tools act as a front end to BIND's DNSSEC tools and focus on key management. They have friendlier messages as they run and pack the many arguments and commands into more intuitive forms.

Vantages tools, vantage-points.org

Vantages is a framework for distributed monitoring that is based on Colorado State University. Its current focus is on operational issues related to DNSSEC, and Vantages can be used to help maintain your DNSSEC deployment.

The project's chief product is vantaged, a daemon that gathers DNSKEY records and compares their values with those obtained by vantaged over the Internet. If lots of vantaged get the same answer, the key is likely to be accurate and not spoofed; a spoofer would have to compromise all sites running the software to get this result. Vantages collects keys from DNS, HTTP, and HTTPS and classifies them into one of four states: confirmed, provisional, unknown, and conflict. It adds confirmed keys to your trusted-keys statement in named.

Vantages has some additional tools as well:

- d-sync monitors the consistency of DNS record keys between parent and child zones, which is especially useful during key rollovers.
- dnsfull determines the MTU between you and any other site. It looks like a traceroute.
- dnskey-grab gets the DNSKEYs for a zone from its authoritative servers.

# Debugging DNSSEC

DNSSEC has been designed to operate with both signed and unsigned zones, and with both DNSSEC-aware and DNSSEC-oblivious name servers. Incremental deployment is possible, and it just works. But not always.

DNSSEC is a distributed system with lots of moving parts. Authoritative servers, client resolvers, and the paths with them can experience problems. A problem seeming locally may originate far away, so tools like Vantages monitor the distributed state of the system. Those tools mentioned in the previous section are helpful.

# Chapter 17 DNS: The Domain Name System

Make sure you route the DNSSEC category to a file in named.conf. It's helpful to separate out the logging. Here is an example specification:

```
channel dnssec {
    "/var/log/named/dnssec.log" versions 4 size 10m;
    print-time yes;
    print-category yes;
    print-severity yes;
    debug 3;
};
```

In BIND you must set the debugging level to 3 to see the steps taken. This logging produces two pages of output per signature. If you are monitoring a busy server, log data from multiple queries will be interleaved. Sorting the mess can be challenging. (Wait, let me re-align the text based on the flow)

For NSD and Unbound, set the verbosity higher than the defaults (0 and 1, respectively) in their config files or, for Unbound, just adjust the verbosity on the fly with **unbound-control**. Like BIND, Unbound must be at log 3 to show the steps.

Once things are OK, set Unbound's val-log-level to 1 to print a one-line error message for each signature that fails. This level of detail helps you keep track of sites that are giving trouble.

If a validating name server cannot verify a signature, it returns a SERVFAIL indication. The underlying problem could be a configuration error by someone at one
