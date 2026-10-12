As you can see, the format of entries are the same for both `chap-secrets` and `pap-secrets`. There are four fields in each line, in the following order:

+   1. `client` — This field contains the name to be used during authentication. This is the username that you get from the ISP.
+   2. `server` — This field contains the name of the remote system to which you are authenticating the local system. If you don't know the server's name, put an asterisk to indicate any server.
+   3. `secret` — This is the secret that your system's PPP server has to send to the remote system to authenticate itself. This is the password you received from the ISP.
+   4. `IP addresses` — This optional field can contain a list of the IP addresses that the local system may use when connecting to the specified server. Typically, this field is left blank because the local system usually gets a dynamic IP address from the server and (therefore) doesn't know what IP address it would use.