# Chapter 7. The X Window System

# 7.4.2. Core X Font System

For compatibility, Red Hat Linux provides the core X subsystem, which uses the X Font Server (xfs) to provide fonts to X applications.

The Free86 server looks for a font specified in the FontPath entry under the Files section of the /etc/X11/xf8Config configuration file. Refer to Section 7.3.1.4 Files for more information on the FontPath entry.

The Free86 server connects to the xfs server on a specified port to acquire font information. For this reason, the xfs service must be running in order to start. For configuring services for a particular runtime, refer to the chapter titled Controlling Access to Services in the Red Hat Linux Customization Guide.

# 7.4.2.1. xfs Configuration

The /etc/rc.init.d/xfs script starts the xfs server. Several options can be configured in the /etc/X11/xfs.config file.

The following is one of the more common options:

+   - alternate-servers — Specifies a list of alternate servers to be used if this font server is not available. A comma must follow every font server in the list.
- catalogue — Specifies an ordered list of fonts to use. A comma must follow every font path before a new font path can be started in the list.
- Use the string unscaled immediately after the font path to mark the unscaled fonts in that path the font server will serve. The load first. Then specify the entry path again, so that other scaled fonts will be loaded.
- client-limit — Specifies the maximum number of clients the font server will serve. By default, this is 10.
- clone-self — Allows the font to clone a new version of itself when the client-limit is hit. By default, this is on.
- default-point-size — Specifies the default font size for any font that does not specify this value. The value for this option is set in dedefs. The default of 120 refers to a 12 point font.
- default-resolutions — Specifies a list of resolutions supported by the XFree86 server. Each resolution in the list must be separated by a comma.
- deferglyphs — Specifies whether to defer loading glyphs (the graphic to visually represent a font). Specifies the path and name of a location where xfs errors are logged.
- error-file — Prevents xfs from listening to particular protocols. By default, this option is set to tcp to prevent xfs from listening on TCP ports for security reasons. If using xfs to serve fonts over the network, remove this line.
- port — Specifies the TCP port that xfs will listen on if no-listen does not exist or is commented out.
- use-syslog — Specifies whether or not to use the system error log.

# 7.4.2.2. Adding Fonts to xfs

To add fonts to the core X font subsystem (xfs), follow these steps: