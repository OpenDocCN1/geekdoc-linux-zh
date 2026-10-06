# UNIX SYSTEM MANAGEMENT PRIMER PLUS

# # Managing Communications Between Varying Levels of Expertise

Nothing is more frustrating to a technical person than having to explain a technical concept or problem in layman's terms—especially during an emergency. Nor is it easy for an advanced technical engineer to listen to a neophyte to explain a problem in technical terms. In the support area, communication between people of varying levels of technical expertise is inevitable. Unless these communication difficulties are resolved, they can have an adverse effect on the efficiency of your support group and their relationships with customers.

# Using Technical Communication Tools

Unless properly trained, help desk employees should not be expected to fully comprehend the code-like mutterings of a systems engineer. Translating them into understandable by lower-level staff—and eventually the customer—is the responsibility of the higher-level staff. At the same time, the help desk staff make sure that they understand the information being communicated to them by higher-level personnel, so they know the status of problems and accurately record that information in their logs.

For example, consider the following problem descriptions, and how they can be effectively communicated to non-technical staff. The technical description is the one support staff enter in the problem's log for other technical staff to see. The plain-English description is for the help desk to use when describing the problem to the customer.

**Problem:** Customer is unable to send email.

**Technical Description:** "The SMTP servers were not configured to accept connections for the 192.168.5/24 subnet."

**Plain-English Description:** "The mail servers were refusing to talk to the network that the customer was on."

**Problem:** Customer says that her dial-up connection is disconnected after only 5 minutes of activity.

**Technical Description:** "The session-timeout RADIUS attribute was set to 300 seconds in this user's profile. It was reset to 43

**Plain-English Description:** "Customer's account was configured to timeout after 5 minutes. The problem was fixed and now she won't be disconnected for 12 hours."

**Problem:** John Smith's FTP session hangs when trying to connect to any FTP server.

**Technical Description:** "John's FTP client doesn't support passive mode, so we had to configure the firewall to allow traffic for TCP port 20 (ftp-data) into our network. We really enforce the use of passive FTP clients."

**Plain-English Description:** "The firewall had to be configured to work with John's FTP program."