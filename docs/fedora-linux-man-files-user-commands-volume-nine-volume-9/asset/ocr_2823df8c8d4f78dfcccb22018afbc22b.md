on port over the secure channel. Implies **-N -T ExitOnForwardFailure** and **ClearAllForwardings** Works with Protocol version 2 only.

-w *local_tun* [: *remote_tun*] Requests tunnel device forwarding with the specified (4) devices between the client (*local_tun*) and the server (*remote_tun*)

The devices may be specified by nurical ID or the keyword “any” which uses the next available tunnel device. If *remote_tun* is not specified, it defaults to “any” See also the **Tunnel** and **TunnelDevice** directives in ssh_config5. If the **Tunnel** directive is unset, it is set to the default tunnel mode, which is “point-to-point”

-X Enables X11 forwarding. This can also be specified on a per-host basis in a configuration file.

X11 forwarding should be enabled with caution. Users with the ability to bypass file permissions on the remote host (for the user’s X authorization database) can access the local X11 display through the forwarded connection. An attacker may then be able to perform activities such as keystroke monitoring.

For this reason, X11 forwarding is subjected to X11 SECURITY extension restrictions by default. Please refer to the **ssh -Y** option and the **ForwardX11Trusted** directive in ssh_config5 for more information.

-x Disables X11 forwarding.

-Y Enables trusted X11 forwarding. Trusted X11 forwardings are not subjected to the X11 SECURITY extension controls.

-y Send log information using the (3) system module. By default this information is sent to stderr.

**ssh** may additionally obtain configuration data from a per-user configuration file and a system-wide configuration file. The file format and configuration options are described in ssh_config5.