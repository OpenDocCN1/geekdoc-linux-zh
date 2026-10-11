# Listing 2.3: continued

```
47: `/*`
48: `    unlink(pth_unix);`
49: `
50:     /*`
51:     `* Form an AF_UNIX Address:`
52:     `*/`
53: `memset(&adr_unix,0,sizeof adr_unix);`
54: `
55:     adr_unix.sun_family = AF_UNIX;`
56: `
57:     strncpy(adr_unix.sun_path,pth_unix,`
58: `            sizeof adr_unix.sun_path-1)`
59: `    [sizeof adr_unix.sun_path-1] = 0;`
60: `
61:     len_unix = SUN_LEN(&adr_unix);`
62: `
63:     /*`
64:     `* Now bind the address to the socket:`
65:     `*/`
66: `    z = bind(sock_unix,`
67: `        (struct sockaddr *)&adr_unix,`
68: `        len_unix);`
69: `
70:     if ( z == -1 )`
71: `        bail("bind");`
72: `
73:     /*`
74:     `* Display all of our bound sockets:`
75:     `*/`
76: `    system("netstat -pa -unix 2>/dev/null"`
77: `        "sed -n '/Active UNIX,/-Proto/p'"`
78: `        "/af_unix/p/");`
79: `
80:     /*`
81:     `* Close and unlink our socket path:`
82:     `*/`
83: `    close(sock_unix);`
84: `    unlink(pth_unix);`
85: `
86:     return 0;`
87: `}`
```

The steps used in Listing 2.3 are as follows:

+   1. Variable `sock_unix` is defined in line 28 to hold the file descriptor for the created socket.