
Figure 7.2 Local port-forwarding settings.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_262_0.png)

After the SSH client has been completely installed, the e-mail client is ready for the secure e-mail architecture.

## Setting Up the E-mail Client

Once the SSH client has been set up, the e-mail client on the road-warrior laptops should be configured. Using Microsoft Outlook Express 4.0 or above, configure as follows:

- 1. Start + Programs + Outlook Express.
- 2. Select Tools from the menu bar and select Accounts.
- 3. Select the Mail tab.
- 4. Select the Add button and choose mail option.
- 5. For Display name, enter the name you would like to have displayed for your e-mail account, such as Mohandas Gandhi. Select Next.
- 6. For E-mail address, enter your e-mail address given to you by your e-mail administrator, such as gandhi@bharat.com. Select Next.
- 7. The next screen should be the E-mail Server Names. There are four steps to complete here:
  - a. If you are using POP3, select POP3 for your incoming mail server (if you are using IMAP, make sure IMAP is selected for your incoming server).
  - b. For the Incoming mail server, enter 127.0.0.1. Remember, you have already set up your port-forwarding steps in the prior section. Once the SSH session has been established, local ports will listen on port 25 and 110. When Outlook Express attempts to connect to 127.0.0.1 on 110, it will be redirected by the SSH client to the e-mail server of the SSH tunnel.
  - c. For the Outgoing mail server, enter 127.0.0.1.
  - d. Select Next.
- 8. Enter your account name given to you by your e-mail administrator, such as Gandhi.
- 9. Enter your password, if you would like to; however, I recommend you leave this blank and allow the application to prompt you for authentication every time you log in. Select Next.
- 10. Click Finish. The e-mail client for secure e-mail has been completed.
- 11. To verify, highlight 127.0.0.1 in the account field and choose the Properties button on the right. Figures 7.3, 7.4, and 7.5 show how the General, Servers, and Advanced tabs should look on your e-mail client.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_263_0.png)

**Figure 7.3** General tab of Outlook Express.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_264_0.png)

**Figure 7.4** Servers tab of Outlook Express.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_264_1.png)

**Figure 7.5** Advanced tab of Outlook Express.

Once you have verified your setting, select OK and Close. You have completed the e-mail client setup for SSH.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_265_0.png)

Figure 7.6 Connection to the SSH server.

## Executing Secure E-mail

At this point, you have completed the necessary steps for secure e-mail. You have configured your SSH server and appropriate firewall rules, configured your SSH client for port forwarding, and configured your e-mail client to use your loopback address.

In order to start using the secure e-mail architecture, open SecureCRT and connect to the SSH server, as shown in Figure 7.6.

To verify the port-forwarding tunnels, type `netstat -an` on the command line, and both port 25 and port 110 should be listening on the IP address `0.0.0.0`, as shown in Figure 7.7.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_265_1.png)

Figure 7.7 Local port-forwarding connections listening on ports 25 and 110.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_266_0.png)

Figure 7.8 Outlook Express.

Once the SSH server has been established, Outlook Express should automatically open. You should automatically be prompted to log in with your correct password, as shown in Figure 7.8.

Once you have authenticated, your e-mail should be downloaded from the e-mail server over the encrypted SSH tunnel.

Note that the e-mail communication will be going through its native protocols, such as SMTP and POP3, to and from the SSH server on the internal network; however, the e-mail communication will be encrypted in the SSH tunnel from the SSH server, over the Internet, to the e-mail client.

Congratulations! You have just implemented a secure e-mail architecture over the Internet.

# Secure File Transfer (SMB and NFS) with SSH

Common file transfer protocols such as SMB (Server Message Block), and NFS (Network File System) are often used in many network environments to share files to and from file servers. For example, Windows networking relies heavily on NetBIOS with SMB for file transfers to and from Windows servers and clients. While the need for SMB is quite important, the attack threats of SMB and NetBIOS greatly increase the security exposures in many Windows networks. While use of NetBIOS with SMB may be appropriate for internal networks, exposure of SMB file sharing to remote users and hostile networks, such as the Internet, is not. Nevertheless, although SMB over the Internet is not appropriate, remote users still need access to corporate file servers, including Windows file servers. Secure remote access is where SSH can be used for secure file access.

In addition to SMB, NFS (over TCP) also is exposed to many security threats in an organization. NFS is a clear-text protocol. Authentication information, as well as payload information, can be sniffed from this protocol. Also, as with SMB, NFS is dangerous to use in hostile networks such as the Internet. NFS vulnerability attacks are abundant; therefore, any use of this protocol can significantly increase the security risk of your organization. Nevertheless, as with SMB, the security vulnerabilities with NFS do not make the desire to gain remote file access over hostile networks any less demanding. While the security threats may be high with this protocol, the demand for remote file access needs to be met. This is also where SSH can be used for secure file access.

The use of SSH can help mitigate some of the issues with vulnerable or clear-text file transfer protocols by using port forwarding with an SSH server to tunnel the SMB and NFS protocols over the Internet inside an SSH tunnel. This not only protects against security attacks and unauthorized sniffing but also offers the ability to enforce two-factor authentication with the SSH connection, thus increasing the overall security of the file transfer architecture.

In this section, I will demonstrate how to implement an SSH architecture with port forwarding to support secure file transfer. The architecture I will be using is shown in Figure 7.9.

Figure 7.9 shows an SSH server, listening on port 22 (SSH), and two internal file servers. The two file servers include a Windows 2000 file server, listening on port 445 (SMB over TCP), a Sun Solaris NFS file server, listening on port 2049 (NFS over TCP), and port 1026 (mountd). The SSH server is located in Internet DMZ off the perimeter firewall, segmented from the internal network. The corporate file servers are located inside the internal network, fully accessible to internal employees for file access.

The second example will assume that the SSH server is a Windows machine running VanDyke Software’s VShell SSH server, that the SSH client is SSH Communications’ SSH2 client running on a Unix platform for the road warriors, and that the file transfer clients are smbclients for SMB and mount for NFS. Any SSH server or SSH client can be used. The example is a random selection from the different SSH applications I have discussed thus far.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_268_0.png)

**Figure 7.9** Secure file-sharing architecture.

## Table 7.1 Firewall Rules That Need to Be Enabled

| RULE NUMBER | SOURCE | DESTINATION | SERVICE | ACTION |
|---|---|---|---|---|
| 1 | Any | SSH-Server | Port 22 | Allow |
| 2 | SSH server | Windows File Server | Port 445 | Allow |
| 3 | SSH server | Solaris NFS file server | Port 2049 Port 1026 | Allow |
| 4 | Any | Any | Any | Deny |

### Setting Up the SSH Server

Since I am using the Vshell SSH server on a Windows platform, no special changes are required. The service will automatically port forward all connections to and from the SSH server. Nevertheless, similar to the first example, there needs to be some specific rules on the adjacent firewall to ensure that port forwarding communications will be allowed. First, on the firewall's external interface (the interface that faces the Internet), connections must be allowed from the outside Internet to the SSH server, specifically port 22 on IP address 11.30.11.21. Second, the firewall's DMZ interface (the interface that connects to the SSH server), needs to allow connections from the SSH server to the internal file servers. Specifically, the rules need to allow the SSH server (11.30.11.21) on any source port to port 445 on the Windows file server (172.16.1.100) and allow the SSH server (11.30.11.21) on any source port to port 2049 and 1026 on the Solaris NFS file server (172.16.1.150). Table 7.1 shows an example of the firewall rules.

After the SSH server has been completely installed and the firewall rules are in place, the SSH server is ready for the secure file transfer architecture.

### Setting Up the SSH Client

Once the SSH server has been set up, the SSH client on the road-warrior Unix laptops should be configured. Using SSH Communications' SSH server version 3.0 or above, configure as follows:

- 1. Change directories to your home directory.
- 2. Since you would like to connect to both file servers, you will need local port-forwarding options for each of them with the use of the -L option
