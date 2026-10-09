# ACTIVITY 13-3
# Configuring the Proxy Server

+   **Before You Begin:**
1. On srvA, you have logged in as root in the GUI.
2. Switch to the CLI.
3. Enter cd /root to navigate to the root directory.
4. Enter yum localinstall /rhe1source/Server/squid-2.6.STABLE21-3.e15.i386.rpm to start installing the Squid package. Enter y to complete the package installation.
5. Clear the terminal window.

**Scenario:**
You are a network administrator in an organization that has different teams handling design, content development, online customer support, and office administration. You have just installed a proxy server. Now, you need to configure the proxy server so that the settings comply with the guidelines in the Internet access policy document provided by the IT manager. The guidelines are are:
- The administrative staff need access to the Internet only during lunchtime on weekdays; other employees must be able to access the Internet all the time.
- No pornographic sites should be accessible.

The administration team is in the 192.168.1.0/255.255.255.0 subnet, and the other teams are in the 192.168.0.0/255.255.255.0 subnet.