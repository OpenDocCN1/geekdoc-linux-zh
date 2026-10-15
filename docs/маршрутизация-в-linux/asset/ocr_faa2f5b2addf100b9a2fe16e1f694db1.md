A common misconception created by the use of modems is that the telephone network is analog given that the modem is converting the computer's digital signal to an analog signal. This is not the case. The analog signal sent over the copper wire from the customer premises to the telephone company is converted to a digital 64kbps signal.

This 64kbps signal is referred to as a DS0 that is then combined (multiplexed) with 23 other DS0s into a 1.54Mbps DS1. The DS1 is often referred to as a T1 or "trunk." The T1 is typically multiplexed with other traffic to be transported via a DS3/T3 (672 DS0s) or higher connection. Figure 12.1 shows how a connection between two modems would operate. Such a network was often used with electronic bulletin board systems in the 1980s and was a basis of worldwide store-and-forward type networks such as Fido. Modem to modem connections are seldom used except by system administrators; however, even this application of modem-to-modem communication is often a second choice to terminal servers. Terminal servers are covered later in this chapter in the "Terminal Servers" section.

![](bbox=[0.12, 0.48, 0.92, 0.62])

The modulation used by the modem must match that of the far end and determines the speed of communication, typically represented in bits per second (bps). Table 12.1 lists some of the common speeds, the modulation standard, and where use of the modulation is likely. In the past, modulation protocols determined interoperability; however, wider support of protocols and improved protocol negotiation allows most modems to have a common protocol that can be used. Additionally, remote access servers, which are covered later, also support a wide base of modulation protocols and error correction protocols.

# Table 12.1 Common Modem Speeds, Standards Body, and Deployment Area

| Modem Speed | Standards Body | Deployment Area |
|---|---|---|
| 300 | Bell 103 | US |
|  | CCITT V.21 | Outside the US |
| 1200 | Bell 212A | US |
|  | CCITT V.22 | Outside the US |
|  | CCITT V.23 | Europe |
| 2400 | CCITT V.22bis | International |
| 9600 | CCITT V.32 | International |