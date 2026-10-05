# 17.11 The NSD/UNBOUND SOFTWARE

With BIND configuration out of the way, we now introduce an alternative DNS server implementation that offers some nice features along with speedy performance. NSD, the Name Server Daemon, was developed by NLNet in 2003. The original intention of the project was to develop an alternative implementation independent of BIND that could be used on root servers, making the root zone more robust through software diversity. Three root servers and top-level domains now use NSD, but you don't have to be a root server or TLD to benefit from NSD's robustness, speed, and simplicity.

Two programs form the core of the NSD software: zonec, a zone file compiler that converts text-format DNS files into databases; and nsd, the name server daemon itself. NSD precomputes and indexes all possible answers to the valid queries it may receive, unlike BIND, which creates its answers on the fly, NSD has the answers in an outgoing packet in a single memory copy, making it incredibly fast.

Unbound is a recursive DNS server that is complementary to NSD. Developed in C by NLNet from a Java implementation by VerSign, Memory, Kire, and EP.NET. NSD and Unbound provide flexible, fast, secure DNS service appropriate for most sites. The NLNet components are not as mature as BIND and do not have many bells and whistles, but they are free for most sites.

ldns, a library of routines that make it easier to write DNS software tools, is also available for use with the NSD and Unbound distributions. It includes a directory of examples: several tools aimed primarily at DNSSEC, a DNSSEC signer tool, and drill, a debugging tool similar to BIND's dig. You can download all them from nlnet.nl. NLNet has also built a tool called Autrust that does RFC5011 rollover and key management. It is being integrated into Unbound; we do not cover it here.

The DNSSEC code in NSD/Unbound is more robust and better than in BIND. It is also faster. For example, Unbound is five times faster than BIND at verifying DNSSEC signatures. BIND still has an edge in some areas, notably in documentation and in extra features. For a truly robust DNS regime, run both!

# Installing and configuring NSD

First, create a user nsd on the system where the nsd name server will run. Then log in as nsd, download the NSD/Unbound packages (currently, three of them: NSD, Unbound, and the separate ldns), and unpack. To install nsd, follow the directions in the doc/README file in the distribution, basically:

```
$ /configure
smake
sudo make install
```