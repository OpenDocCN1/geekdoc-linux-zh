
## VGA Card Types

- **cirrus**  
  Cirrus Logic GD5446 Video card. All Windows versions starting from Windows 95 should recognize and use this graphic card. For optimal performance, use 16 bit color depth in the guest and the host os. (This one is the default)

- **std**  
  Standard VGA card with Bochs VBE extensions. If your guest os supports the VESA 2.0 VBE extensions (e.g. Windows XP) and if you want to use high resolution modes (>= 1280x1024x16) then you should use this option.

- **vmware**  
  VMware SVGA-II compatible adapter. Use it if you have sufficiently recent XFree86/XOrg server or Windows guest with a driver for this card.

- **qxl**  
  QXL paravirtual graphic card. It is VGA compatible (including VESA 2.0 VBE support). Works best with qxl guest drivers installed though. Recommended choice when using the spice protocol.

- **tcx**  
  (sun4m only) Sun TCX framebuffer. This is the default framebuffer for sun4m machines and offers both 8-bit and 24-bit colour depths at a fixed resolution of 1024x768.

- **cg3**  
  (sun4m only) Sun cgthree framebuffer. This is a simple 8-bit framebuffer for sun4m machines available in both 1024x768 (OpenBIOS) and 1152x900 (OBP) resolutions aid at people wishing to run older Solaris versions.

- **virtio**  
  Virtio VGA card.

- **none**  
  Disable VGA card.

## Command Line Options

- **portair**: Rotate graphical output 90 deg left (only PXA LCD).
- **rotate deg**: Rotate graphical output so deg left (only PXA LCD).
- **vga type**: Select type of VGA card to emulate. Valid values for type are listed above.
- **full-screen**: Start in full screen.
- **g width height [xdepth]**: Set the initial graphical resolution and depth (PPC, SPARC only).
- **vnc display [ , option [ , option [ , ...]]]**:  
  Normally, QEMU uses SDL to display the VGA output. With this option, you can have QEMU listen on VNC display *display* and redirect the VGA display over the VNC session. It is very useful to enable the usb tablet device when using this option (option `usb-tablet`). When using the vnc display, you should use the `-k` parameter to set the keyboard layout if you are not using en-us. Valid syntax for the display is *host:d*

  TCP connections will only be allowed from *host* on display *d*. By convention the TCP port is 5900+*d*. Optionally, *host* can be omitted in which case the server will accept connections from any host.

  **unix:path**  
  Connections will be allowed over UNIX domain sockets where *path* is the location of a unix socket to listen for connections on.

  **none**  
  VNC is initialized but not started. The monitor change command can be used to later start the VNC server.

Following the display value there may be one or more option flags separated by commas. Valid options are:

### VNC Options

- **reverse**  
  Connect to a listening VNC client via a “reverse” connection. The client is specified by the display. For reverse network connections (*host:d*,*reverse*), the *d* argument is a TCP port number, not a display number.

- **websocket**  
  Opens an additional TCP listening port dedicated to VNC Websocket connections. By definition the Websocket port is 5700+*display*. If *host* is specified connections will only be allowed from this host. As an alternative the Websocket port could be specified by using *websocket=port*. TLS encryption for the Websocket connection is supported if the required certificates are specified with the VNC option *x509*.

- **password**  
  Require that password based authentication is used for client connections. The password must be set separately using the `set_password` command in the `pcsys_monitor`. The syntax to change your password is: `set_password <protocol> <password>` where `<protocol>` could be either “vnc” or “spice”.

  If you would like to change `<protocol>` password expiration, you should use `expire_password <protocol> <expiration-time>` where *expiration time* could be one of the following options: *now*, *never*, *+seconds* or UNIX *time* of expiration, e.g. *+60* to make password expire in 60 seconds, or *1335196800* to make password expire on “Mon Apr 23 12:00:00 EDT 2012” (UNIX *time* for this date and time).

  You can also use keywords “now” or “never” for the expiration time to allow `<protocol>` password to expire immediately or never expire.

- **tls**  
  Require that client use TLS when communicating with the VNC server. This uses anonymous TLS credentials so is susceptible to a man-in-the-middle attack. It is recommended that this option be combined with either the *x509* or *x509verify* options.

- **x509=/path/to/certificate/dir**  
  Valid if *tls* is specified. Require that x509 credentials are used for negotiating the TLS session. The server will send its x509 certificate to the client. It is recommended that a password be set on the VNC server to provide authentication of the client when this is used. The path following this option specifies where the x509 certificates are to be loaded from. See the **vnc_security** section for details on generating certificates.

- **x509verify=/path/to/certificate/dir**  
  Valid if *tls* is specified. Require that x509 credentials are used for negotiating the TLS session. The server will send its x509 certificate to the client, and request that the client send its own x509 certificate. The server will validate the client’s certificate against the CA certificate, and reject clients when validation fails. If the certificate authority is trusted, this is a sufficient authentication mechanism. You may still wish to set a password on the VNC server as a second authentication layer. The path following this option specifies where the x509 certificates are to be loaded from. See the **vnc_security** section for details on generating certificates.

- **sasl**  
  Require that the client use SASL to authenticate with the VNC server. The exact choice of authentication method used is controlled from the system / user's SASL configuration file for the 'qemu' service. This is typically found in /etc/sasl2/qemu.conf. If running QEMU as an unprivileged user, an environment variable `SASL_CONF_PATH` can be used to make it search alternate locations for the service config. While SASL auth methods can also provide data encryption (eg GSSAPI), it is recommended that SASL always be combined with the 'tls' and 'x509' settings to enable use of SSL and server certificates. This ensures a data encryption preventing compromise of authentication credentials. See the **vnc_security** section for details on using SASL authentication.

- **acl**  
  Turn on access control lists for checking of the x509 client certificate and SASL identity. For x509 certs, the ACL check is made against the certificate's distinguished name. This is something that looks like `C=GB, O=ACME, L=Boston, CN=bob`. For SASL identity, the ACL check is made against the username, which depending on the SASL plugin, may include a realm component, eg `bob@realm`. When the **acl** flag is set, the initial access list will be empty, with a deny policy. Thus no one will be allowed to use the VNC server until the ACLs have been loaded. This can be achieved using the acl monitor command.

- **lossy**  
  Enable lossy compression methods (gradient, JPEG, ...). If this option is set, VNC client may receive lossy framebuffer updates depending on its encoding settings. Enabling this option can save a lot of bandwidth at the expense of quality.

- **non-adaptive**  
  Disable adaptive encodings. Adaptive encodings are enabled by default. An adaptive encoding will try to detect frequently updated screen regions, and send updates in these regions using a lossy encoding (like JPEG). This can be really helpful to save bandwidth when playing videos. Disabling adaptive encodings restores the original static behavior of encodings like Tight.

- **share=[allow-exclusive|force-shared|ignore]**  
  Set display sharing policy. 'allow-exclusive' allows clients to ask for exclusive access. As suggested by the rfb spec this is implemented by dropping other connections. Connecting multiple clients in parallel requires all clients asking for a shared session (vncviewer: -shared switch). This is the default. 'force-shared' disables exclusive client access. Useful for shared desktop sessions, where you don't want someone forgetting to specify -shared to disconnect everybody else. 'ignore' completely ignores the shared flag and allows everybody to connect unconditionally. Doesn't conform to the rfb spec but is traditional QEMU behavior.

i386 target only:

- **win2k-hack**  
  Use it when installing Windows 2000 to avoid a disk full bug. After Windows 2000 is
