# # Setting Up Dial-Up Networking 293

![](bbox=[0.218, 0.125, 0.545, 0.388])

**Figure 1-12:** Click Activate in the Network Configuration dialog box to establish the PPP connection.

+   7. Select the connection name, and then click Activate.
8. When you're done, click Deactivate to turn the PPP connection off.

# ## Configuring CHAP and PAP authentication

The PPP server on your system has to authenticate itself to the ISP's PPP server before the PPP connection can get fully up and running. *Authentication requires proving that you have a valid account with the ISP; essentially providing a username and a secret (that is, a password).* PPP specifies two ways of exchanging the authentication information between the two ends of:

+   **Handshake Authentication Protocol (CHAP)** requires the remote end to send a randomly generated challenge string with the remote server's name. The server's name then sends back a response that includes its name and a value that checks the secret and the challenge, using a one-way hash function. The remote system then checks that value against its own calculation of the expected hash value. If the values match, the authentication succeeds; otherwise it terminates the connection. In this case, the name and secret are stored in the /etc/secrets file. Note that the remote system can repeat the CHAP authentication any time the PPP link is up.

+   **Password Authentication Protocol (PAP)** is like the normal login process. When using PAP, the local system repeatedly sends a username (name) and password (secret) until the remote system acknowledges the authentication or ends the connection. The name and secret are stored in the /etc/ppp/pap-secrets file. Note that the username and password are sent in the clear (that is, unencrypted).

Book IV
Chapter 1
Connecting to the Internet