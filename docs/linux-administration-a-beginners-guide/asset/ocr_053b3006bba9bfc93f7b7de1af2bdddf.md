The Post Office Protocol, or POP for short, is a standardized mechanism that workstations of any operating system can use to download mail from a mail server. POP was created as a result of two developments:

+   The proliferation on the Internet of non-UNIX PCs lacking the capability to run a fully capable SMTP server such as Sendmail.

+   The proliferation of workstations connected to the Internet via dial-up facilities that are rarely connected 100% of the time.

Under POP, mail servers running an SMTP server can accept messages and store them in a mail spool; users on any type of workstation with a POP-compliant mail reader can then connect to the POP server (which can read the mail spool written to by the SMTP server) and download their mail. When a user wants to send e-mail, the workstation can contact the local SMTP server and relay outgoing messages to it. See Figure 16-1.

This chapter discusses the POP Version 3 (POP3) protocol in detail, along with the security implications of supporting it. We then step through the process of downloading, compiling, and installing it.

![](bbox=[0.14, 0.47, 0.87, 0.94])

Figure 16-1. Sending and receiving mail with SMTP and POP