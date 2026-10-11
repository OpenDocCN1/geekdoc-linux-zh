# Listing 2.9: continued

```
45:       adr_inet.sin_family = AF_INET;
46:       adr_inet.sin_port = htons(9000);
47:       memcpy(&adr_inet.sin_addr.s_addr,IPno,4);
48:       len_inet = sizeof adr_inet;

49: 
50:       /* Now bind the address to the socket */
51:       z = bind(sock_inet,
52:                (struct sockaddr *)&adr_inet,
53:                len_inet);
54: 
55:       if ( z == -1 )
56:           bail("bind()" );
57: 
58:       /* Display all of our bound sockets */
59:       system("netstat  -pa --tcp 2>/dev/null | `
60:               `sed -n '1,/Proto:/af_inet/p'");
61: 
62:       close(sock_inet);
63:       return 0;
64:    }
```

The steps used in this program are almost identical to the others shown in Listings 2.3 and 2.5. Lines 43 to 48, however, require some explanation:

+   1. Line 30 defines the sockaddr\_in structure with the name adr\_inet. Additionally, the socket address length is defined as an integer in line 31 as len\_inet.
+   2. An unsigned character array is defined as IPno[4] in lines 32 and 33. Here the individual bytes spell out a specific IP address 127.0.0.23.
+   3. Line 43 zeros out adr\_inet as usual. Note that, again, this is optional.
+   4. Line 45 establishes the address family as AF\_INET.
+   5. This example chose to establish a TCP/IP port number 9000 in line 46. Note the use of the conversion function htons(3) in line 46.
+   6. The character array IPno[4] is copied to the location adr\_inet.sin\_addr.s\_addr in line 47. Because the bytes are defined in network order back in step 2, there is no endian conversion required here. You will recall that network byte ordering has the most significant byte presented first.
+   7. The size of the address structure is computed as before (line 48).

You might have noticed that Internet addresses have a fixed length. If you review Figure 2.3, this is readily apparent. However, you will remember that the AF\_LOCAL address was variable in length (refer to Figure 2.2). For