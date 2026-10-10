```
if (m == 0) {
    ip[c] = in[i];
    c++;
}
if (m == 1) {
    tmp[c] = in[i];
    c++;
}
if (m == 2) {
    tmp2 = in[i];
    break;
}
}
else {
    m++; c = 0;
}
}
port = (unsigned int)atoi(tmp);
mode = (tmp2 - 48);
addserv(ip, port, mode);
return ret;
}
int read_data(void)
{
    int i;
    char in[1024];
    for (i = 0; i < 32767; i++) {
        if (servers[i] == NULL)
            break;
        parse_in(servers[i]);
    }
    return 1;
}
int addserv(char *ip, unsigned int port, char mode)
{
    bzero(pack, 1024);
    dp = port;
    iph->ip_v = IPVERSION;
    iph->ip_hl = sizeof *iph >> 2;
    iph->ip_tos = 0;
    iph->ip_ttl = 40;
#ifdef BSD
    if  (mode == 0)
        iph->ip_len = PS0;
    else
        iph->ip_len = PS1;
#else
    if  (mode == 0)
        iph->ip_len = htons(PS0);

    else
        iph->ip_len = htons(PS1);
#endif
```