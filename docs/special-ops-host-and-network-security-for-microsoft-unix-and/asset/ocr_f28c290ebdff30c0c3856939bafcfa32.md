+   - Information disclosure vulnerabilities may reveal information that could be used to facilitate other types of attacks.

+   - Denial of service vulnerabilities allow an attacker to remotely disable or shut down your Web services.

+   - Buffer overflow vulnerabilities, although complicated, are very serious because they can allow an attacker to execute programs under the context of the SYSTEM account.

+   - Directory traversal vulnerabilities allow intruders to traverse the file system and possibly execute programs under the context of the anonymous Web user account.

+   - Cross-site scripting vulnerabilities allow one user to exploit a Web application to gather information or gain access rights of other users.

# # Preparing the Operating System

+   - Remove unused Windows components and disable unnecessary services to reduce the attack surface of the server.

+   - Segment the hard drive into separate partitions to prevent directory traversal attacks and always use NTFS when formatting a partition.

+   - Lock down COM and database access by removing unused drivers and securing sensitive COM components.

# # Securing Web Services

+   - In its default state, IIS is vulnerable to a number of different attacks.

+   - Run the IIS Lockdown Wizard, a free tool that uses templates to accomplish the best steps to harden an IIS server, and which installs URLScan, a tool for blocking certain types of Web requests based on certain HTTP elements.

+   - Global IIS Registry settings should be set to the recommended values.

+   - When IIS is first installed, two Web sites are created: a default Web site and an administration site. Lock down both.

+   - Disable Web-based printing to avoid adding unnecessary exposure to a production Web server.