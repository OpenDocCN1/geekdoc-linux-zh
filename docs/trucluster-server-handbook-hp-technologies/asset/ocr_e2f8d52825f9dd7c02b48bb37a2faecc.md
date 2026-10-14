```
# netstat -an
Active Internet connections (including servers)
Proto Recv-Q Send-Q Local Address          Foreign Address        (state)
tcp      0      0 192.168.0.69:4034      192.168.0.2:53         TIME_WAIT
tcp      0      0 192.168.0.69:4035      192.168.0.2:53         TIME_WAIT
tcp      0  300 192.168.0.69:23        192.168.0.2:1184       ESTABLISHED
tcp      0      0 192.168.0.70:53        *:*                    LISTEN
tcp      0      0 192.168.0.69:53        *:*                    LISTEN
tcp      0      0 127.0.0.1:53           *:*                    LISTEN
tcp      0      0 10.0.0.2:53            *:*                    LISTEN
tcp      0      0 *:596                  *:*                    LISTEN
...(lots more)
tcp      0      0 192.168.0.69:1153      *:*                    LISTEN
tcp      0      0 127.0.0.1:1153         *:*                    LISTEN
tcp      0      0 10.0.0.2:1153          *:*                    LISTEN
tcp      0      0 192.168.0.69:1152      *:*                    LISTEN
tcp      0      0 127.0.0.1:1152         *:*                    LISTEN
tcp      0      0 10.0.0.2:1152          *:*                    LISTEN
tcp      0      0 *:830                  *:*                    LISTEN
tcp      0      0 *:2049                 *:*                    LISTEN
tcp      0      0 *:1022                 *:*                    LISTEN
tcp      0      0 *:61                   *:*                    LISTEN
tcp      0      0 *:111                  *:*                    LISTEN
udp      0      0 *:2049                 *:*                    
udp      0      0 *.37                   *:*                    
udp      0      0 192.168.0.70:53        *:*                    
udp      0      0 192.168.0.69:53        *:*                    
udp      0      0 127.0.0.1:53           *:*                    
udp      0      0 10.0.0.2:53            *:*                    
udp      0      0 *:111                  *:*                    
udp      0      0 *:1139                 *:*                    
udp      0      0 *:1144                 *:*                    
udp      0      0 *:1145                 *:*                    
udp      0      0 *:1146                 *:*                    
udp      0      0 192.168.0.70:123       *:*                    
udp      0      0 192.168.0.69:123       *:*                    
udp      0      0 127.0.0.1:123          *:*                    
...(lots more)
```

# 16.10.3 Dynamically Assigned Port Numbers

The port numbers can be associated with an actual application by examining the /etc/services file (see section 16.10.1). Note that not all numbers are found in this file. For example, examining the /etc/services file for a telnet entry shows that telnet is associated with TCP port number 23. But there are two sides to a connection. What port number is used for the other side of the telnet connection? The server side (running telnetd) will be associated with port number 23. The client side will have allocated a port that is reserved for user requests.

These client side ports are dynamically chosen by the networking software in the kernel. Since the clients are usually not cluster members, there tend to be plenty of these "ephemeral" ports for the clients to use. But have we ever said that a cluster cannot be a client?