Correct answer and explanation: D. D is the correct answer because nmap can be used to scan a subnet and list devices connected to the network.

Incorrect answers and explanations: A, B, and C. A is incorrect because wireshark only monitors traffic that makes it to your network interface and may not see devices that are idle. B is incorrect because snort monitors traffic seen by your local network interface and typically only pays attention to traffic that matches a list of known suspicious patterns. C is incorrect because tripwire monitors files on the local host for potentially unauthorized changes.

**4.  You just finished downloading the latest version of your favorite program and want to make sure that it downloaded correctly by comparing it with the hash file posted on the download site. What program would you use to make sure the file is exactly what it should be?**

+   *   **A.** filecheck my_download
+   *   **B.** md5sum -c my_download.md5
+   *   **C.** diff my_download.md5 gpg my_download
+   *   **D.** gpg my_download

Correct answer and explanation: B. B is correct because md5sum -c will calculate the hash value of the file listed in the given file and compare it with the hash value in the file.

Incorrect answers and explanations: A, C, and D. A is incorrect because filecheck isn’t a valid Linux command. C is incorrect because the diff command is used to compare two local files. D is incorrect because gpg would be used to confirm the file is correct if it has been signed by the owners’ private key using your copy of his public key.

**5.  You are going to start working from home occasionally and need full access to your office Linux workstation as well as a Windows PC via your VPN connection. What remote access software should you consider?**

+   *   **A.** ssh
+   *   **B.** X11
+   *   **C.** VNC
+   *   **D.** PCAnywhere

Correct answer and explanation: C. C is the correct answer because VNC works between unlike operating systems and provides full desktop access.