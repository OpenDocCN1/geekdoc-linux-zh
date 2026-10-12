These virus scanners can usually handle HTTP and FTP traffic too. The user's client application (e.g. Web browser) is configured to use the virus-scanner as a proxy. The client sends the request to the proxy, which retrieves the page and virus-scans it, and then returns the scanned page to the client.

# Content filtering (content scanning)

To perform virus scanning, the proxy server needs a full understanding of the relevant protocol. For example, to scan incoming Web pages, the scanner must be a Web proxy server, be able to handle all the different types of HTTP requests, and forward all the retrieved pages to the client. It also needs a full understanding of the different data encodings, so that embedded files as well as the top-level pages can be scanned correctly. Compressed archives such as Zip files or UNIX tar archives are often sent via HTTP, so the scanner must understand these formats, be able to extract the individual entries in the archives, and re-insert disinfected files into the archive when it has finished scanning.

Because the scanner already contains all this infrastructure, enhancing the system to scan for things other than viruses is relatively straightforward. Scanning systems now let you perform some or all of the following:

+   block the Web page or discard the e-mail if it contains particular keywords (e.g. if an outgoing message contains “Here’s a copy of my resume,” or an incoming Web page contains the phrase “red hot teen girls” – you get the idea)
+   discard particular attachment types, e.g. Visual Basic or executable programs
+   limit Web download sizes, or defer sending large e-mail messages until night-time, to reduce the load on your Internet connection during busy periods
+   define a whole security and usage policy, saying who can send what to whom, when, etc.

Systems like these are used primarily by organizations for their own financial, legal, religious, or other reasons to control what their users are allowed to access. There are other, similar systems that control Web downloads for the user's benefit. An example is the Proxomitron, which is highly configurable. Some of its options are:

+   don't download banner advertisements (saves bandwidth and display time)
+   remove pop-up windows
+   automatically change fonts and colors on the page (e.g. if you have a sight disability or merely good taste)
+   limit the information that a server can obtain from your browser about you and your PC
+   remove specified types of JavaScript from pages, especially scripts that add advertisements or breach your privacy
+   disable animation of GIF images (saves CPU on your browser).

Virus and content scanning does slow down traffic. Users can notice this on large HTTP transfers, but not with e-mail, as message receipt is not interactive.