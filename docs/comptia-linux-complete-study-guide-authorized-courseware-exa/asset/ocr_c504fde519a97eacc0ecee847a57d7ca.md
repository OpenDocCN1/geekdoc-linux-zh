**TABLE 8.2 Port Numbers, Their Purposes, and Typical Linux Servers (continued)**

| Port Number | TCP or UDP | Purpose | Example Linux Servers |
|---|---|---|---|
| 995 | TCP | POP-3 over SSL | Dovecot, Qpopper, popa3d |
| 5900+ | TCP | Remote Framebuffer (RFB) | Virtual Network Computing (VNC): OpenVNC, TightVNC |
| 6000–6007 | TCP | The X Window System (X) | X.org-X11, XFree86 |

$^1$Port 465 is officially registered for URD; however, it's also commonly used as a secure e-mail delivery port, although this isn't the officially designated purpose of this port.

One key distinction in TCP/IP ports is that between *privileged ports* and *unprivileged ports*. The former have numbers less than 1024. Unix and Linux systems restrict access to privileged ports to *root*. The idea is that a client can connect to a privileged port and be confident that the server running on that port was configured by the system administrator and can therefore be trusted. Unfortunately, on today's Internet, this trust would be unjustified based solely on the port number, so this distinction isn't very useful. Port numbers greater than 1024 may be accessed by ordinary users.

# Clients and Servers

An important distinction is the one between *clients* and *servers*. A *client* is a program that initiates a network connection to exchange data. A *server* listens for such connections and responds to them. For instance, a Web browser, such as Firefox or Opera, is a client program. You launch the program and direct it to a Web page, which means that the Web browser sends a request to the Web (HTTP) server at the specified address. The Web server sends back data in reply to the request. Clients can also send data, as when you enter information in a Web form and click a Submit or Send button.

The terms *client* and *server* can also be applied to *entire computers* that operate mostly on one or the other role. Thus, a phrase such as *Web server* is somewhat ambiguous—it can refer either to the Web server program or to the computer that runs that program. When this distinction is important and unclear from context, I clarify it (for instance, by referring to “the Web server program”).

Fortunately, for basic functioning, you need to do nothing to configure ports on a Linux system. You may have to deal with this issue if you run unusual servers, though, because you may need to configure the system to link the servers to the correct ports. This can sometimes