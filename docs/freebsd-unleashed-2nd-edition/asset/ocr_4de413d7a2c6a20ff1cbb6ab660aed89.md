# CHAPTER 24

# Configuring E-mail Services

What's the Internet without e-mail? Probably not even the Web, with its flashy graphics and its commercial opportunities, has quite the usefulness and cachet of the Internet's oldest application, electronic mail. Every Unix server in the world has e-mail capabilities built in to it—not just the capability for users to send and receive mail, but for the system itself to act as a full-fledged mail server. FreeBSD is no exception.

The catch is that configuring Sendmail, the venerable SMTP server application that forms the e-mail backbone of Unix and the Internet, is perhaps the most daunting system administration task you'll face. After all, Sendmail is perhaps unique among server software in that it has a config file for *its config file*. But don't worry, this chapter outlines and gives you a solid grounding in the use of Sendmail. You learn how to configure and manage the program for secure and reliable performance, but you're spared the exhaustive coverage of details that could make Sendmail seem overwhelming or needlessly complex.

This chapter also covers another side of e-mail: POP and IMAP. These are the protocols remote clients use to receive e-mail. Fortunately, their use is nowhere near as complicated as Sendmail.

# Introduction to SMTP

The Simple Mail Transfer Protocol (SMTP) is one of the oldest protocols on the Internet—nearly as old as e-mail itself. SMTP's purpose is to transfer plain-text messages from one host to another. This transfer often occurs in sequence, as when a dial-up client running Windows sends an e-mail

# IN THIS CHAPTER

+   * Introduction to SMTP
+   * Mail Transfer Agents (MTAs) and Mail User Agents (MUAs)
+   * Configuring Basic E-mail Services with Sendmail
+   * Understanding Relaying
+   * Introduction to POP3
+   * Configuring a POP3 Server with Qpopper
+   * Configuring an IMAP Server with IMAP-uw
+   * E-mail for Standalone Workstations
+   * A Look at Some Sendmail Replacements