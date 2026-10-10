# CGI Pifering

**Synopsis:** Hackers can download and view CGI source code.

**Hack State:** Code theft.

**Vulnerabilities:** Apache (version 1.3.12 in version 6.4 of SuSE)

**Breach:** Default installation and configuration of the Apache HTTP server daemon enables hackers to download CGI scripts directly from the Internet. Basically, the scripts stored in the /cgi-bin/ directory can be accessed, downloaded, and viewed, as opposed to host execution only.

# Directory Listing

**Synopsis:** Hackers can exploit an Apache Win32 vulnerability to gain unauthorized directory listings.

**Hack State:** Unauthorized directory listing.

![](bbox=[0.12, 0.38, 0.76, 0.76])

**Figure 9.6** Apache HTTP Server for Windows.

**Vulnerabilities:** Apache (version 1.3.3, 1.3.6, and 1.3.12) Win32.

**Breach:** The exploit is caused when a path is too long as Apache searches for the HTTP startup file (e.g., index.html). The result is an unauthorized directory listing, regardless of the startup file existence.

# Denial-of-Service Attack