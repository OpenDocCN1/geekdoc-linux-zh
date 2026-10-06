# Part IV: Fedora and RHEL Network and Server Setup

+   1. Select Add to the Create VPN Connection window and select Forward to continue.

+   2. For this example, select OpenVPN Client (Cisco VPN client is also available), and click Forward. You are asked to enter VPN connection information.

+   3. Fill in the following information for your openvpn connection:
   * **Connection name** — The name or anything you like.
   * **Gateway address** — The name or IP address of the openvpn server that is acting as the gateway for your VPN connection.
   * **Connection type** — Select the default X.509 Certificates (if you are using the example server from Chapter 16). You can also select Pre-shared key, Password Authentication, or X.509 with Password Authentication.
   * **CA file** — Identify the location of the root certificate you certify your server (possibly to /etc/openvpn/keys/ca.crt).
   * **Certificate** — Identify the location of the client certificate you copied from the key server (possibly to /etc/openvpn/keys/client01.crt).
   * **Key** — Identify the location of the client key you copied from the key server (possibly to /etc/openvpn/keys/client01.key).

If everything works, select Apply to apply your new VPN connection.

+   4. If the openvpn server is up and running, try your new VPN connection. Select the NetworkManager agent. Choose VPN Connects and select the name of the new VPN connection you configured.

NetworkManager is still a work in progress, so the automated features may not extend as far as you would like. For example, when you change wired and wireless interfaces, besides bringing VPN interfaces up or down, you may also want to unmount and mount shared file systems. Work is underway in this area, but has not yet included in any formal release.

# Understanding Local Area Networks

Connecting the computers in your organization via a LAN can save you a lot of time and money. By putting a small amount of money into networking hardware, even in a small configuration (five or six users), can save you from buying multiple printers, backup media, and other hardware. A large, shared Internet connection and you no longer need multiple mediums and Internet connections.

With a LAN, you don't have to run down the hallway with your file on a disk or USB thumb drive to print on your friend's printer. Information that had to wait for the mailroom to make the rounds can be sent in an instant to anyone (or everyone) on your LAN.

With a LAN, you begin to open the greatest potential of Linux — its ability to act as a server on a network. Because Fedora and RHEL are more robust and feature-rich than