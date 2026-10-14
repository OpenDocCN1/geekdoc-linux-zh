# Anonymous session limit Guest session limit

Anonymous users and guest users can be limited to the specified time. This option correlates to the limit-time directive.

# Maximum login failures

This option allows you to define the number of failed login attempts to allow before a "too many login failures" message is presented to the user and the FTP connection is closed. This option configures the loginfails directive and defaults to 5.

# Can switch groups?

If this option is turned on, a user may switch to a new group after login. The user will then have the privileges of the new group. This configures the private directive and defaults to off.

# Networking

Here you configure a few of the networking-related options for WU-FTPD.

# TCP window sizes

This option configures the window size of TCP packets for the data connection. This may be useful if clients are PPP dial-up users, as a smaller TCP window can provide faster transfers. Usually this does not need to be modified. This option correlates to the tcpwindow directive.

# Addresses for PASV connections

Allows control of the address reported in response to a PASV command. This does not alter the address that the daemon listens on, only the address it reports to clients on a passive connection. This option configures the passive address directive.

# Ports for PASV connections

Configures the port numbers which may be used for passive data connections. You may select port ranges for specific networks. When a control connection matches the network specified, a randomly selected port from the range provided will be used for the daemon to listen on. This feature allows firewalls that limit open ports to be used, while still provided FTP services. This option corresponds to the passive ports directive.