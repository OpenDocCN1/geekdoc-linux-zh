> **NOTE** Despite the fact that the SuSE manual says that ISDN supports only the Euro-ISDN, some firms in North America wrote the drivers for their cards to work for Linux on the NI-1 protocol. Please check http://www.spellcast.com for more information if you are a North American user.

# Supported ISDN Cards

Linux supports a large number of active and passive ISDN cards. Appendix B, "Hardware Compatibility List," contains a list of the supported ISDN cards. For passive cards to work, you have to connect them to your Phone Branch Exchange (PBX), which might get them to work.

# ISDN Connection Software Requirements

Package requirements:

Series a:

+   - modules
+   - net_tool
+   - netcfg
+   - kernmod (only if you don't want to recompile your kernel)
+   - isapnp (for PnP controllers)
+   - pciutils (for automatic configuration of PnP controllers)
+   - nkita (Packages nkita and nk1tb have security holes in all SuSE versions up to 6.2; you might want to upgrade them from the SuSE FTP site. The new secure version is available on the accompanying CD.)
+   - nk1tb

Series n:

+   - ppp
+   - inetcfg
+   - i41

Kernel requirements:

+   - Character devices, standard/generic (dumb) serial support
+   - Network device support, dummy net driver support
+   - Network device support, PPP or SLIP