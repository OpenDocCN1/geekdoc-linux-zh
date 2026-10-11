# # Immediate Solutions

# ## Configuring Networking

To configure your networking, follow this general order of events:

+   1. Where you start depends on what type of connection you are setting up:
+      - If you are setting up a modem connection, see “Setting Up Dial-Out Connections”, later in this chapter.
+      - To set up the basic networking information for an internal LAN connection, go to either “Manually Configuring Basic Static Networking For A LAN” or “Configuring Basic Networking With Linuxconf For A LAN.”

> **NOTE:** If you need to set up a LAN and a modem connection that connects that LAN to the outside world, start by configuring the LAN internals and configure the PPP connection last.

+   2. Test the connections. Try talking to the outside world. If you just set up a LAN, make sure the machines can talk both inside and outside the network.
+   3. Shore up your security—as discussed in Chapter 9—before you continue. Or, at least do some of the initial work in this area, for now.
+   4. Set up your domain name resolution, as discussed in Chapter 11.
+   5. Set up the other Internet and network services, such as email, Web, and so on.
+   6. Finish shoring up your security.

| Related solutions: | Found on page: |
|---|---|
| Shutting Off Unnecessary Daemons And Background Processes | 264 |
| Shutting Off Unnecessary Non-Daemon Network Services | 267 |
| Restricting Network Access With tcp_wrappers | 267 |
| Removing Unnecessary Packages | 279 |
| Analyzing Logs | 281 |
| Preparing For A Breach | 282 |
| Securing Passwords With Crack | 284 |

(continued)