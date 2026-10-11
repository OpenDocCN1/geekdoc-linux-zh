Listing 5.2: continued

```
39:    /*
40:     * Obtain the address of the socket:
41:     */
42:    len_inet = sizeof adr_inet;
43:
44:    z = getsockname(s,
45:        (struct sockaddr *)&adr_inet,
46:        &len_inet);
47:
48:    if ( z == -1 )
49:        return NULL;    /* Failed */
50:
51:    /*
52:     * Convert address into a string
53:     * form that can be displayed:
54:     */
55:    snprintf(buf,bufsiz,
56:        "%s:%u",
57:        inet_ntoa(adr_inet.sin_addr),
58:        (unsigned)ntohs(adr_inet.sin_port));
59:
60:    return buf;
61:}
62:
63:/*
64: * Main Program:
65: */
66:int
67:main(int argc,char **argv,char **envp) {
68:    int z;            /* Status return code */
69:    int sck_inet;    /* Socket */
70:    struct sockaddr_in adr_inet;/* AF_INET */
71:    int len_inet;    /* length */
72:    char buf[64];    /* Work buffer */
73:
74:    /*
75:     * Create an IPv4 Internet Socket:
76:     */
77:    sck_inet = socket(AF_INET,SOCK_STREAM,0);
78:
79:    if ( sck_inet == -1 )
80:        bail("socket()" );
81:
82:    /*
83:     * Create an AF_INET address:
84:     */
```