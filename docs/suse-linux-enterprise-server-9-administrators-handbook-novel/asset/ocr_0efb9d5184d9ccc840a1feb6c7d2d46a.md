# TIP

If you plan on tackling Sendmail, you'll want to make sure you have a good resource for installing and configuring the server. The sendmail book (ISBN 1-56592-222-0) from O'Reilly & Associates, coauthored by Sendmail developer Eric Allman, is considered to be the definitive guide on the subject.

SLES 9 ships with several mail servers, among them Sendmail and Postfix. Developed by Dr. Wietse Venema of IBM’s Thomas J. Watson Research Center (Yorktown Heights, New York), Postfix attempts to be a fast, easy-to-administer, and secure replacement for Sendmail. SLES 9 installs Postfix by default, even for a base system configuration. Therefore, the discussion in this section is about Postfix.

# NOTE

Two other favored email server software packages (commonly referred to as Message Transfer Agents or MTAs) among the Linux/Unix community are Qmail (http://www.qmail.org) and Exim (http://www.exim.org). However, they are not included with SLES.

# WARNING

The Postfix package conflicts with those of Sendmail and Exim. Therefore, if you have Postfix installed, it must first be uninstalled before installing Sendmail or Exim. (If you install, for instance, Sendmail via YaST, the dependencies check will warn you of the conflict and permit you to specify a resolution action.)

One of the best things about Postfix is that it can be set up quickly and easily without sacrificing security. The following steps lead you to a Postfix quick-start:

+   1. Install the Postfix package (using YaST or rpm) if it is not already installed. You can find it on your SLES CD1 or download the latest version from http://www.postfix.org.

# NOTE

If you are installing Postfix from the source tarball, you should be aware that the INSTALL file and many of the readme files (in the README files directory) use backspace characters to emulate bold text. Depending on your terminal’s setting, you may see text similar to Postfix, and so on. You will definitely see these characters if you open the file in a text