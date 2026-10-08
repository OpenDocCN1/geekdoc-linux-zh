person, however, will always insist that she be allowed to telnet<sup>21</sup> in from her home system that has a dynamic IP assigned by her ISP at the start of each session.

Because she is running an old version of Linux (or Windows or MacOS for that matter) and will not install SSH.<sup>22</sup> she talks to the Network Administrator about allowing the firewall to pass telnet requests to her Linux workstation "at the office." Sys beware. Pizza, beer or sodas, and tries to Fry's bribes are all common. Resist at all costs.

A cracker determines her work system's IP by network scanning for systems (or simply trying all IP addresses on the network), and cracks her box with an old vulnerability because she was too busy to harden her system as he deemed. (She had promised the Network Administrator last year that she would harden her system "real soon.") Recall that the firewall allows telnet to work her box. Now that the cracker is start penetrating the other boxes because they are not guarding against an attack from *inside* the firewall.

This type of attack, a very serious one that many organizations are vulnerable to, can be protected in several ways. The only option is to be strict about firewall policy, regardless of the inconvenience to users. I hate unnecessarily severe measures let us consider some other techniques.

The user could be required to use SSH. The Administrator might help her set up SSH. Frequently, a user's willingness to migrate is that she does not know how, and fears it will take a long time. A few minutes of your time might be well spent. A bribe may work in your favor

She could required to start each session using telnet to access a known secure system that is outside her firewall and has that telnet upgraded to a secure one. Note that good-to-break passwords are necessary here. I discuss password selection in "Avoiding Weak and Default Passwords" on page 36. Note that her system from her home system to the secure system will still be vulnerable to sniffing; anyone sniffing then she will be able to break into her system by seeing what password she supplies to SSH.

Her work system could possibly be separated from other systems by a different firewall, although this would still leave her system vulnerable. Thus, if her system is cracked, the intruder cannot then travel to the other systems (assuming that other than her system, good security measures have been taken). Clearly this the most desirable solution for her system is vulnerable.

If her system contains proprietary source code, engineering documents, manufacturing procedures, patent applications, client lists, marketing plans, the company directory (that headhunters could use for raiding and crackers could use for social engineering), negotiating strategies, or a host of other important files, a cracker breaking into her system could be disastrous.

She could arrange for a reverse DNS map to map whatever dynamic IP she gets from her home system's to a fully qualified host name, then gets placed in her work system's /etc/hosts.allow file, used by TCP Wrappers on her work system.

+   21. An excellent alternative to telinet, which is telnet over SSL.

+   22. SSH is available for Linux, UNIX, Windows, MacOS. VMS, and Java. I ported SSH2 to an ancient Linux 1.2 kernel in two hours.