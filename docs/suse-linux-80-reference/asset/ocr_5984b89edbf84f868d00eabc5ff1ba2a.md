```
NULLCLIENT=""
```

A null client is a machine that can only send mail. It receives no mail from the network and it does not deliver any mail locally. A null client typically uses POP or NFS for mailbox access.

**3ddiag** — For 3Ddiag.

```
SCRIPT_3D="switch2mesasoft"
```

This variable specifies the script used to create the necessary symbolic links to the correct OpenGL libraries or extensions. These scripts are located in `/usr/X11R6/bin`. Possible values are:

+   - `no` — execute no script.
+   - `switch2mesasoft` — emulation of Mesa-Software (works with all graphics cards)
+   - `switch2mesa3dfx` — Mesa/Glide
+   - `switch2nvidia_glx` — XFree86 4.x/NVIDIA_GLX (NVIDIA_GLX/NVIDIA_kernel)
+   - `switch2xf86_glx` — XFree86 4.x/DRI

Use 3Ddiag to determine the correct settings. See Section *OpenGL — 3D Configuration* on page 169.

**xdmsc** — Using X terminals.

```
START_RX="no"
```

First, edit `/etc/inittab` to remove the comment from the line with `/sbin/init.d/rx`. Then RX_XDMCP and RX_RHOST must be set. Finally, set START_RX to yes if you want to have an X terminal.

```
RX_XDMCP="broadcast"
```

xdm control protocol: query, indirect, or broadcast. For query or indirect, set RX_RHOST.

```
RX_RHOST=""
```

xdm host necessary if RX_XDMCP set to query or indirect.

```
RX_DSP=""
```

Optional DISPLAY number, e.g., :1 or :2. Default is DISPLAY :0.

```
RX_BPP=""
```

Optional color depth of local X server.

```
RX_CLASS=""
```

**windowmanager** — Windowmanager.

```
DEFAULT_WM="kde"
```

Here, set the default window manager, such as kde, gnome, or fvwm.