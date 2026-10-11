```
Listing 3.3: continued

```
55:         (struct sockaddr *)&adr_inet,
56:                 len_inet);
57:
58:         if ( z == -1 )
59:                 bail('bind()');
60:
61:         /* Display our socket address */
62:         system("netstat -pa --tcp 2>/dev/null|"
63:                 "| grep inetaddr");
64:
65:         return 0;
66: }
```
```

NOTE
If netstat(1) command on your system does not support the options used in lines 62 and 63 of Listing 3.3, substitute the following call if you have lsof installed:
```c
system("lsof -i tcp | grep inetaddr");
```

The general program structure is very similar to the ones used in the previous chapter. However, the steps used to set up the socket address are a bit different. They are

+   1. The socket address structure is zeroed out in line 40. This is an optional step, but many find that this helps debugging should it become necessary.
+   2. The address family is established as AF_INET in line 42.
+   3. The port number has been established as port 9000 in this example (line 43).
+   4. The function inet_addr(3) is called in line 46 to convert the string constant "127.0.0.95" into a network 32-bit address. This value is stored into the socket address member adr_inet.sin_addr.s_addr.
+   5. The value returned from the conversion in step 4 is tested to see whether it matches the value INADDR_NONE in line 48. If it does, this indicates that the value provided in the C string was not a good Internet IP number (the program bails out in line 49 if this happens).
+   6. Finally, the length of the socket address is established in line 51 as before.

The above procedure has established the socket address in the variable adr_inet. This is later passed to bind(2) in line 54, which has not been covered yet. The bind(3) call just applies the address to the socket (the full discussion will otherwise be deferred for now).