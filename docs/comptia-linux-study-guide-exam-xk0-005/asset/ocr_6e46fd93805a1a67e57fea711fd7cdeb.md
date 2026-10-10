> **NOTE**
> Be aware that the `wxr1nfnfo` command will hang if you are running a Wayland session instead of an X session. Press `Ctrl+C` to exit out of the hung command.

Although Wayland is replacing X as the default display server on many Linux systems, the X server will be around for a while. Thus, understanding them both is invaluable not only for certification purposes but also to work effectively.

# ## Using Remote Desktops

Sitting down at a monitor directly attached to your Linux server is a rarity nowadays. Most servers are either rack-mounted systems in condition-controlled environments or virtual machines running on those rack-mounted systems. To access these servers, a user from a desktop in another room typically employs the text-based OpenSSH utility. However, there are times you need a fully functional desktop environment.

Remote desktop software uses a client-server model. The server runs on the remote Linux system, and the client runs on the local system. For example, say you need to access a Linux virtual machine located on a server somewhere else in the office building. You could use your laptop, which is running the remote desktop client software, to log into the Linux virtual machine, which is running the remote desktop server software, and get a full-fledged desktop experience over the network.

In the following sections we'll take a look at some common remote desktop implementations for Linux. They include VNC, Xrdp, NX, and SPICE.

# ## Viewing VNC

Virtual Network Computing (VNC) was developed by the Olivetti & Oracle Research Lab. It is multiplatform and employs the Remote Frame Buffer (RFB) protocol. This protocol allows a user on the client side to send GUI commands, such as mouse clicks, to the server. The server sends desktop frames back to the client's monitor. RealVNC Ltd., which consists of the original VNC project team developers, now trademarks VNC.

> **NOTE**
> If you are using KVM virtual machines (covered in Chapters 28 and 29), then typically, by default, you access their desktop environment via VNC. However, there are other options available, such as SPICE, which is covered later in this chapter.

The VNC server offers a GUI service at `TCP` port `5900 + n`, where `n` equals the display number, usually `1` (port `5901`). On the command line, you point the VNC client (called a `viewer`) to the VNC server's hostname and `TCP` port. Alternatively, you can use the display number instead of the whole `TCP` port number. The client user is required to enter a predetermined password, which is for the VNC server, not Linux system authentication. Once