# 31. Communications

You will almost certainly want to go online or otherwise communicate with other computer systems. Most systems today are sold with the necessary hardware to connect to other systems, such as a modem or a network card. You connect this hardware to the outside world via a telephone line or network connection.

This chapter includes recipes for connecting your Linux system to the Internet with an ISP, using fax services, and making serial connections with a modem.

For more information on this subject, see The Linux Network Administrator's Guide [http://metalab.unc.edu/mdw/LDP/nag/nag.html].

# 31.1 Connecting to the Internet

PPP
DEB: ppp
RPM: ppp
WWW: ftp://cs.anu.edu.au/pub/software/ppp/

There are several ways to connect a Linux box¹ to the Internet. Digital Subscriber Line (DSL) service, cable modems, and dial-up connections with ISDN or analog modems are currently the most popular methods. Each of these services has its own hardware and software requirements. Generally, you get these services by subscribing to them from an Internet Service Provider, or ISP.

For up-to-date, detailed instructions for using these services on Linux-based systems, the relevant HOWTOs published by the Linux Documentation Project [http://tldp.org/] remain the definitive guides (see Recipe 2.8.6 [Reading System Documentation and Help Files], page 50):

+   - ISP Hookup HOWTO, by Egil Kvaleberg
+     http://tldp.org/HOWTO/ISP-Hookup-HOWTO.html
+   - DSL HOWTO for Linux, by David Fannin et al.
+     http://en.tldp.org/HOWTO/DSL-HOWTO/

¹ A computer is sometimes called a box, particularly when one aspect of it is being described; therefore when you hear talk about a "Linux box" you know it's just a computer that is running Linux. This slang is particularly popular among users of UNIX flavors, but people do talk of Windows boxes.