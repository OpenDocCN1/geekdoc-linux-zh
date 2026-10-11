examining the state of *xinetd*. Example 10-41 displays a sample *servers* entry in the `/etc/xinetd.conf` file. Notice that this service is of the `INTERNAL UNLISTED` type, which means that it is an internal function of *xinetd* and that it is not listed in `/etc/services`. The port number used is completely arbitrary.

# **Example 10-41** Sample servers Entry

```
```
   service servers
   {
      type          = INTERNAL UNLISTED
      socket_type   = stream
      protocol      = tcp
      port          = 9997
      wait          = no
      only_from     = 172.17.33.111
      wait          = no
   }
```
```

Note that this service is available only from the specific IP address 172.17.33.111, which should be the IP address of the server itself. This disallows any other host from obtaining this information from this server. The security ramification here is very simple—if this information were available to be read by others on other systems, it could well lead to an exploit based on the knowledge of which daemons are currently running. It is perhaps ill advised to run this server at all except for debugging purposes, since any user on 172.17.33.111 is able to obtain this information by executing `telnet 172.17.33.111 9997` as shown in Example 10-42 (line numbers added for clarity). Note that *xinetd* simply provides the information and exits, providing no interactive connection. The output shown in Example 10-42 tells us that there are two running `telnet` daemons (lines 5 and 31), one with the PID of 5931 and the other with the PID of 5961 (lines 6 and 32, respectively). There is one `ftp` daemon (line 18) running with the PID of 5960 (line 19). Some connection information and logging information is provided for each running daemon. Probably not the sort of information you want floating around, and, in general, for security reasons you may want this turned off, except perhaps on tightly secured systems. To turn it off, make sure that no entry of the type shown in Example 10-41 is present in `/etc/xinetd.conf` file.

# **Example 10-42** Example Output of servers Service

```
```
1      $ telnet topcat 9997
2      Trying 172.17.33.111...
3      Connected to topcat.
4      Escape character is `^]'.
5      telnet server
6      pid = 5931
7      start_time = Sat Apr 17 10:32:15 1999
8      Connection info:
9          state = CLOSED
10        service = telnet
11        descriptor = 20
12        flags = 3
```
```