ISP, essentially providing a username and a *secret* (that is, a password). PPP specifies two ways of exchanging the authentication information between the two ends of the connection:

+   ◆ **Challenge Handshake Authentication Protocol (CHAP)** requires the remote end to send a randomly generated challenge string along with the remote server’s name. The local system looks up the *secret*, using the server’s name; then it sends back a response that includes its name and a value that combines the *secret* and the challenge, using a one-way hash function. The remote system then checks that value against its own calculation of the expected hash value. If the values match, the authentication succeeds; otherwise, the remote system terminates the connection. In this case, the name and *secret* are stored in the */etc/ppp/chap-secrets* file. Note that the remote system can repeat the CHAP authentication any time while the PPP link is up.

+   ◆ **Password Authentication Protocol (PAP)** is like the normal login process. When using PAP, the local system repeatedly sends a username (name) and password (*secret*) until the remote system acknowledges the authentication or ends the connection. The name and *secret* are stored in the */etc/ppp/pap-secrets* file. Note that the username and password are sent in the clear (that is, unencrypted).

The Linux PPP server supports both types of authentication. For both PAP and CHAP, the information that the PPP server needs is a name and a *secret* — a username and password pair. This authentication information is stored in the following configuration files:

+   ◆ */etc/ppp/chap-secrets* stores the information for CHAP. Here’s what a typical chap-secrets file looks like:

```
```
# Secrets for authentication using CHAP
# client      server      secret      IP addresses
"naba"        *          "mypassword"
```
```

+   ◆ */etc/ppp/pap-secrets* stores the information for PAP. Here’s a typical pap-secrets file:

```
```
# Secrets for authentication using PAP
# client      server      secret      IP addresses
"naba"        *          "mypassword"
```
```

As you can see, the formats of the entries are the same for both chap-secrets and pap-secrets. Four fields are in each line, in the following order:

+   ◆ *client*: This field contains the name that is used during authentication. You get this name from the ISP.