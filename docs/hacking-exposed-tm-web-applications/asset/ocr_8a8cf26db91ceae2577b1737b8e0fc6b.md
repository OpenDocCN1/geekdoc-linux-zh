# Chapter 12: Web Client Hacking

http://www.microsoft.com is in the Internet zone it has periods in its name. When you visit a site within a zone, the specific security settings for that zone apply to your activities on that site—for example, Run ActiveX Controls may be allowed. Furthermore, the most important zone to configure is the Internet zone, since it contains all the sites a user is likely to visit. Of course, if you add sites to any other zone, this rule doesn't apply. Be sure to carefully select trusted and untrusted sites when populating the other zones—if you choose to do so at. (Typically, zones will be populated by network administrators for corporate LAN users).

To configure security for the Internet zone, open Tools | Internet Options within IE (or the Internet Options control), highlight the Internet zone, click Default, and move the slider to an appropriate point. We recommend setting it to High and then using the Custom Level button to go back and disable all other active content, plus a few other usability tweaks, as shown in Table 12-1. Note that these ActiveX controls, including those marked as safe, but do not block JavaScript(ActiveScript is enabled).

Of course, disabling ActiveX may result in viewing sites that depend on controls for special effects. One highly visible example is Macromedia's pop ActiveX control. If you want to get all that sound and animation from Shockwave, you will have to enable ActiveX (unless, of course, you use Netscape's browser, where Shockwave comes in the form of a plug-in). Another ActiveX-oriented site that most users will likely visit is Microsoft's Windows Update (WU), which uses ActiveX to scan the user's machine and to download and install appropriate patches. WU is a great idea—it saves huge amounts of time ferreting out individual patches (especially security

| Category | Setting Name | Recommended Setting | Comment |
|---|---|---|---|n| ActiveX controls and plugin-ins | Script ActiveX controls marked “safe for scripting” | Disable | Client-resident “safe” controls can be exploited. |
| Cookies | Allow per-session cookies (not stored) | Enable | Less secure but more user friendly. |
| Downloads | File download | Enable | IE will automatically prompt for download based on the file extension. |
| Scripting | ActiveXScripting | Enable | Less secure but more user friendly. |

Table 12-1. Recommended Internet Zone Security Settings (Custom Level Settings Made After Setting Default to High)