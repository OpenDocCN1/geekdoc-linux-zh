```
```
85:    memset(&adr_inet, 0, sizeof adr_inet);
86:    adr_inet.sin_family = AF_INET;
87:    adr_inet.sin_port = htons(9000);
88:    inet_aton(“127.0.0.24”,&adr_inet.sin_addr);
89:    len_inet = sizeof adr_inet;
90:
91:    /*
92:    * Now bind the address to the socket:
93:    */
94:    z = bind(sock_inet,
95:        (struct sockaddr *)&adr_inet,
96:        len_inet);
97:    if ( z == -1 )
98:        bail(“bind()”);
99:
100:    /*
101:    * Now test our sock_addr() function:
102:    */
103:    if ( !sock_addr(sock_inet,buf,sizeof buf) )
104:        bail(“sock_addr()”);
105:
106:    printf(“Address is ‘%s\n”,buf);
107:
108:    close(sock_inet);
109:    return 0;
110: }
```
```

Listing 5.2 shows how getsockname(2) could be used by a library C function. Much of the main() program is review for you, because it is very similar to the main() program in Listing 5.1. The general steps used in the main() program are

+   1.  Declarations for the socket sock_inet, the address adr_inet, and the address length len_inet are given in lines 69 to 71.
+   2.  A character array buffer buf[64] is declared in line 72 for use later in the program.
+   3.  The socket is created by socket(2) in line 77.
+   4.  A socket address is established in lines 85 to 95 with the use of the bind(2) function call.
+   5.  The sock_addr() function is called inside the if statement in line 103. If the function returns a null pointer, the statement in line 104 is executed and the program will terminate.
+   6.  If Step 5 succeeds, however, the buffer buf[] will contain a string that represents the socket address for socket sock_inet. The printf(3) call in line 106 reports this result.