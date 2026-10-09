# HTTP_CONNECTION

The `HTTP_CONNECTION` variable is set to the type of connection being used by the client and the server. For example:

```
HTTP_CONNECTION = Keep-Alive
```

This states that the client is capable of handling persistent connections using Keep-Alive and currently using it.

# SERVER_PORT

The value of the `SERVER_PORT` variable tells a CGI program which server port is currently being used to access the program. A sample of this is:

```
SERVER_PORT = 80
```

If a CGI program creates URLs that point back to the server, it might be useful to include the port address, which is found as the value of this variable in the URL.

# REMOTE_HOST

The `REMOTE_HOST` variable tells a CGI program about the IP address or IP name of the client, as follows:

```
REMOTE_HOST = dsl-666.isp24by7.net
```

Note that if the Apache server is compiled with the MINIMAL_DNS option, this variable is not set.

# REMOTE_PORT

This port number is used in the client-side of the socket connection:

```
REMOTE_PORT = 1163
```

I have not yet seen any use for this variable.

# REMOTE_ADDR

The `REMOTE_ADDR` variable is the IP address of the client system:

```
REMOTE_ADDR = 192.168.1.100
```