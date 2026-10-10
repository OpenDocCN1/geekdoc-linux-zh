![](bbox=[0.12, 0.05, 0.55, 0.65])

2.  The web browser configures its proxy to 127.0.0.1 on port 8080. Web browser makes a web request. It sends the request to the local port 8080 on the client’s (lookback address (127.0.0.1).

1.  SSH client makes a connection to the SSH client which is connecting port 8080 from the client to the SSH server.

3.  The port forwarded connection takes the web request and forwards to the SSH server over the established SSH tunnel (over port 22).

4.  Forwarded web request reaches the HTTP proxy services (port 8080) from the SSH connection.

5.  Proxy server sends the request to the Internet.

# Figure 9.17  Data flow for secure Web communication.