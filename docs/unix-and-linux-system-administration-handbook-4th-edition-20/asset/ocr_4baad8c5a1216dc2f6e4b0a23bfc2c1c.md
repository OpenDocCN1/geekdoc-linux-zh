# VNC: Virtual Network Computing

In the late 1990s, a few people at AT&T Labs in Cambridge, UK, developed a system for remote desktop access called VNC. Their idea was to marry the simplicity of a dumb terminal with the modern world of window systems. In contrast to X11, the VNC protocol does not deal with individual applications. Instead, it creates a virtual desktop (or provides remote access to an existing desktop) as a unit.

AT&T published the VNC software under a liberal license source. This openness allowed other folks to hop on the bandwagon and create additional server and viewer implementations, as well as protocol improvements that reduced the consumption of network bandwidth. Today, VNC viewers are available for most devices that provide some means for graphical display. VNC servers for UNIX, Linux, and now are widely available.

The UNIX VNC server implementation is essentially a graphics adapter emulator that plugs into the X.Org Windows server. Running a vncserver on UNIX creates a new virtual desktop in the self-contained world of the UNIX machine. You can use a VNC viewer to access that desktop remotely. We recommend taking advantage of the vncpassword command before starting the server for the first time to establish a connection password.

The VNC protocol is stateless and bitmap based. Therefore, viewers can freely connect and disconnect. Moreover, several viewers can access the same server at the same time. This last feature is especially useful for remote support and training setups. It also facilitates shared console access for system administration.

VNC servers in the Windows world do not normally create an extra desktop; they simply export the Standard Windows desktop as it is displayed on screen. The main application for this technology is remote support.

These days, the original authors of the VNC protocol are running their own project, RealVNC (realvnc.com). The UltraVNC project is concentrating on the Windows domain with a very fast and feature-rich Windows-based VNC server implementation, and TightVNC is working on improved compression ratios. These groups talk with each other, so features tend to cross-pollinate among the various implementations.

The VNC protocol has been designed with extensibility in mind. All combinations of viewers and servers can work together; they pick the best protocol variant that both sides understand. Implementation-specific features (such as file transfer) can only be accessed by a server and client running from the same.

# Windows RDP: Remote Desktop Protocol

Ever since Windows 2000 Server, every Windows box has the technical ability to provide graphical remote access to several users at the same time. The remote