# ## Security Focus

Similar to Rootshell, the Security Focus Web site ([http://www.securityfocus.com](http://www.securityfocus.com)) is a full-disclosure site on security issues pertinent to all operating systems. The site is actively maintained; additions to its list of security issues occur almost daily. It also has links to security-related stories around the Internet.

# ## ODDS AND ENDS

Before we jump into the next chapter, I want to bring up two security issues that have nothing to do with Linux but are and forever will be problematic.

The first is security through obscurity. This phrase describes the behavior of people who foolishly believe that by not telling anyone about what's there or how something is done, their system is secure. This simply is not true. Programs can be reverse-engineered, and probes can tell more about the insides of a system or network than we'd ever want revealed. A classic example of why security through-obscurity doesn't work is PGP (Pretty Good Privacy, [http://www.pgp.com](http://www.pgp.com)). Because of its source code, and because underlying algorithms have been revealed to the world and thereby examined by countless cryptography experts, PGP is considered the most secure means of storing information. No proprietary cryptography system has ever reached this level of trust before.

The second issue is social engineering: the process by which a would-be intruder starts with a telephone before taking to the keyboard. It's remarkable what can be learned by making a few phone calls, showing the slightest bit of authority, and asking unsuspicious people for information. Reporters often use this technique for getting the inside scoop on news stories, because they know the average insider is far less likely to be ready to handle probing questions than a public relations representative. Social engineering also works for questions about passwords, network infrastructure, operating systems, and so on.

The only way to help keep social engineering from getting through your site's security is by keeping your system's users educated and aware. They should be warned against revealing critical information to anyone who calls up asking for it. Policies need not be complicated to be effective; for example, "The MIS department will never ask for your password. If anyone does ask for your password, report it immediately."

Security is one of those topics about which you can never say enough. In the course of writing this chapter, I considered touching on many topics that were clearly beyond the scope of the book. Exploring most of these subjects would require adding many more chapters.

Don't fail to take an expansive role in exploring the issues of your system's security. It is an arguably time-consuming task, but it is one that cannot be ignored in this era of complex networks and operating systems. If your environment is like most today, you're probably running several different operating systems and need to contend with security for all of them.