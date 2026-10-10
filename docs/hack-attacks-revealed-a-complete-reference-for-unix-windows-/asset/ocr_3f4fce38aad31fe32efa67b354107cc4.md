```
```
}
printf("Slinging Packets... \n");
src.s_addr = inet_addr(argv[1]);
if (src.s_addr == -1) {
    printf("Invalid source IP: %s\n", argv[1]);
    exit(-1);
}
s = socket(AF_INET, SOCK_RAW, IPPROTO_RAW);
if (s == -1) {
    perror("socket");
    exit(-1);
}

fl = 1;
ret = setsockopt(s, IPPROTO_IP, IP_HDRINCL, &fl, sizeof(int));
if (ret == -1) {
    perror("setsockopt");
    exit(-1);
}

bzero((char *)&addr, sizeof(addr));
addr.sin_family = AF_INET;
read_data();
printf("UnFed.\n");
}
int parse_in(char *in)
{
    int i, n, c, m, ret;
    char ip[16], tmp[6], mode, tmp2;
    unsigned int port;
    bzero(ip, 16); bzero(tmp, 6); mode = 0; port = 0; n = 0; c = 0; m = 0;
    tmp2 = 0;
    for (i = 0; i < strlen(in); i++) {
        if (in[i] != ' ') {
            if (in[i] != ':') {
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
            } else {
                m++; c = 0;
            }
        }
    }
    port = (unsigned int)atoi(tmp);
```
```

515