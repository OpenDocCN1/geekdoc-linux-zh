# 26.12 Miscellaneous

# Other dial-up scenarios

The two scenarios we covered in detail are dial-up to surf the net from home, and connecting to the HQ LAN from a hotel room using a dial-up ISP. Dial-up can be useful in other circumstances, to set up temporary or semi-permanent non-Ethernet connections within an organization, e.g.

+   - connecting home users to HQ, or connecting a remote office to HQ. By not using the Internet you can avoid some security issues. If the remote office or home users is close to the HQ, your phone company may have special arrangements (e.g. Centrex) that let one location phone another free, as though they were just extensions within the same office. That can make this a very cheap option
+   - building a small test network to check out dial-up systems and configurations (see below)
+   - connecting a machine with a broken network card, using a phone and modem, or a direct serial cable, to enable important data (or network drivers) to be transferred to or from the damaged system
+   - using a direct serial cable to connect a workgroup or department in a separate but adjacent building, e.g. across the road. (Stevens in his book describes how he used a SLIP link for this, although nowadays you'd probably use a wireless link instead of a serial cable.)
+   - using Microsoft’s Internet Connection Sharing (ICS) to link several machines at one location (home or small office) to elsewhere, as described in Module 23.11.

In all these examples you're using a phone link with two modems or a direct serial cable to connect a dial-up system at one end to a dial-in server at the other end (Figure 26.30). We haven't covered setting up a dial-in server, but we give some references in the Notes. On NT, RAS includes a dial-in server, so if you've set up a dial-up RAS client, you will find the server side easy.

![](bbox=[0.12, 0.62, 0.89, 0.9])