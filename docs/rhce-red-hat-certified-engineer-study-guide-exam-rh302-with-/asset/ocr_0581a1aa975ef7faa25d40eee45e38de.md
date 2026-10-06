![](bbox=[0.158, 0.116, 0.353, 0.281])

n general, a host that is part of a network is subject to more frequent and greater security threats than a stand-alone host. And, in general, larger networks are subject to greater security risks than smaller networks. Internet host, for example, faces a variety of threats. However, by controlling access to a network host, you can reduce its exposure to security threats.

Red Hat Linux provides three principal mechanisms for controlling access to a host:

**TCP Wrappers** By configuring TCPWrappers, you can restrict the hosts allowed to access a host's services.

**Pluggable Authentication Module (PAM) Facility** By configuring the Pluggable Authentication Module (PAM) facility, you can restrict the users allowed to log in to a host.

**ipchains Firewall** You can restrict access to the ports used by services by configuring ipchains firewall.

This chapter explains the first mechanisms: TCP wrappers and the PAM facility, which is usually known simply as PAM. In addition, it explains the Network Information Service (NIS) and the Lightweight Directory Access Protocol (LDAP), two mechanisms that allow you to centrally control user accounts and other system information. Chapter 30, “Configuring a Firewall Using ipchains,” explains the third mechanism.

# # The inetd Service

The TCP wrappers facility operates in conjunction with the inetd service. This section explains the inetd service; it explains how to configure TCP wrappers, which work with the inetd service.