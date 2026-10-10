
![](img/c99d6f526a5f9fa62f2c34daada85ad7_275_0.png)

**Figure 7.14** Secure management architecture.

The third example will assume that the SSH server is a Unix machine running SSH Communications’ SSH server, that the SSH client is SecureCRT running on a Windows platform for the remote administrators, and that the management clients are a Terminal Services client, VNC client, and a pcAnywhere client.

> **NOTE** Any SSH server and SSH client can be used; my example is a random selection from the different SSH applications I have discussed thus far.

## Setting Up the SSH Server

Since I am using the SSH Communications’ SSH server on a Unix platform, no special changes are required. The service will automatically port forward all connections to/from the SSH server. Nevertheless, as with the first example, some specific rules need to be implemented on the adjacent firewall to ensure that port-forwarding communications will be allowed. First, the firewall’s external interface (the interface that faces the Internet) must allow connections from the outside Internet to the SSH server, specifically port 22 on IP address 11.30.11.21. Second, the firewall’s DMZ interface (the interface that connects to the SSH server) needs to allow connections from the SSH server to the internal management servers. Specifically, the rules need to allow the SSH server (11.30.11.21) on any source port to port 3389 on the Windows Terminal server (10.1.0.100), allow the SSH server (11.30.11.21) on any source port to port 5901 on the Linux VNC server (10.1.0.150), and allow the SSH server (11.30.11.21) on any source port to port 5631 and 5632 on the pcAnywhere server 10.1.0.200). Table 7.2 shows an example of the firewall rules.

After the SSH server has been completely installed and the firewall rules are in place, the SSH server is ready for the secure management architecture.

### Table 7.2 Firewall Rules That Need to Be Enabled

| RULE NUMBER | SOURCE | DESTINATION | SERVICE | ACTION |
|---|---|---|---|---|
| 1 | Any | SSH server | Port 22 | Allow |
| 2 | SSH server | Windows Terminal server | Port 3389 | Allow |
| 3 | SSH server | Linux VNC server | Port 5901 | Allow |
| 4 | SSH server | pcAnywhere server | Port 5631, Port 5632 | Allow |
| 5 | Any | Any | Any | Deny |

## Setting Up the SSH Client

Once the SSH server has been set up, the SSH client for the remote administrators should be configured. Using SecureCRT 4.0 or above, configure as follows.

1. Select Start -> Programs -> SecureCRT -> SecureCRT.
2. Choose File -> Quick Connect.
3. Select SSH2 for the Protocol field.
4. Enter 11.30.11.21 for the Hostname field.
5. Enter 22 for the Port field.
6. Enter the correct username, such as Shreya, in the Username field.
7. Make sure the Save Session box is checked.
8. Select Connect, and log in to the SSH server with the appropriate password.
9. After the session has been established, disconnect the session by choosing File -> Disconnect.
10. Select File -> Connect and highlight the 11.30.11.21 option.
11. Right-click 11.30.11.21 and then select properties.
12. Highlight the Port Forwarding section.

Now that the setup is complete, you can add the local port-forwarding options.

13. Select Add to display the Port Forwarding options.
14. Enter Terminal Server for the Name field.
15. In the Local subsection, make sure "Manually select local IP address on which to allow connections" is unchecked.
16. In the Local subsection, enter 3389 for the Port field.
17. In the Remote subsection, make sure "Destination host is different from the SSH server" is checked.
    a. Enter 10.1.0.100 for the Hostname field.
18. In the Remote subsection, enter port 3389 for the Port field.
19. In the Application subsection, you can either leave it blank or enter the path for the Terminal Services client. If you decide to put in the path, it will execute the Terminal Services client automatically. If you leave it blank, you will have to execute the Terminal Services client manually.
20. Select OK.

Now that the terminal services local port-forwarding option is set up, the Linux VNC server local port-forwarding option can be set.

21. Select **Add** to display the Port Forwarding options.
22. Enter **VNC Server** for the Name field.
23. In the Local subsection, make sure "Manually select local IP address on which to allow connections" is unchecked.
24. In the Local subsection, enter **5901** for the Port field.
25. In the Remote subsection, make sure "Destination host is different from the SSH server" is checked.
    a. Enter **10.1.0.150** for the Hostname field.
26. In the Remote subsection, enter **port 5901** for the Port field.
27. In the Application subsection, you can either leave it blank or enter the path for the VNC client. If you decide to put in the path, it will execute the VNC client automatically. If you leave it blank, you will have to execute the VNC client manually.
28. Select **OK**.

Now that the VNC local port-forwarding option is set up, the pcAnywhere local port-forwarding option can be set.

29. Select **Add** to display the Port Forwarding options.
30. Enter **pcAnywhere** for the Name field.
31. In the Local subsection, make sure "Manually select local IP address on which to allow connections" is unchecked.
32. In the Local subsection, enter **5631** for the Port field.
33. In the Remote subsection, make sure "Destination host is different from the SSH server" is checked.
    a. Enter **10.1.0.200** for the Hostname field.
34. In the Remote subsection, enter **port 5631** for the Port field.
35. In the Application subsection, you can either leave it blank or enter the path for the pcAnywhere client. If you decide to put in the path, it will execute the pcAnywhere client automatically. If you leave it blank, you will have to execute the pcAnywhere client manually.
36. Select **OK**.

Since pcAnywhere requires two ports, you will have to add a second local port forward.

37. Select Add to display the Port Forwarding options.
38. Enter **pcAnywhere2** Server for the Name field.
39. In the Local subsection, make sure “Manually select local IP address on which to allow connections” is unchecked.
40. In the Local subsection, enter **5632** for the Port field.
41. In the Remote subsection, make sure “Destination host is different from the SSH server” is checked.
    a. Enter **10.1.0.200** for the Hostname field.
42. In the Remote subsection, enter port **5632** for the Port field.
43. You can leave the Application subsection blank.
44. Select OK.

The result should look like Figure 7.15.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_279_0.png)

**Figure 7.15** Local port-forwarding settings.

After the SSH client has been completely installed, the management clients are ready for the secure management architecture.

## Setting Up the Management Clients

As with the SSH server, no special configuration is required on the management clients. Each client, including the Terminal Services client, the VNCViewer, and the pcAnywhere client, is a standalone command-line client that can be used seamlessly with SSH. As with the e-mail client in the first example, instead of directing things to the real servers, all connections will be directed locally to the loopback interface, specifically 127.0.0.1, to connect to the local port forwards established by the SSH connection, which will then take those connections and forward them to the appropriate servers over the SSH connection.

## Executing Secure Management

At this point, you have completed the necessary steps for secure management. You have configured your SSH server and appropriate firewall rules, configured your SSH client for port forwarding, and configured your management clients to use your loopback address.

To start using the secure management architecture, execute SecureCRT and connect and authenticate to the SSH Communications' SSH server, as shown in Figure 7.16.

After authenticating, verify the port-forwarding tunnels on the SSH connection by typing **netstat -an** on the command line. Ports 3389, 5631, 5632, and 5901 should be listening on the loopback address, as shown in Figure 7.17.

![](img/c99d6f526a5f9fa62f2c34daada85ad7_280_0.png)

**Figure 7.16** The connection to the SSH server.
