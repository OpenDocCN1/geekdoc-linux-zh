# Hacking Custom Web Applications • Chapter 11

+   SQL introduces an additional level of complexity with its capability to execute multiple statements. SQL injection attacks are on the rise, and are gaining in popularity.

+   <HIDDEN> fields keep no secrets from even the just curious browsers.

+   Cookies reside with end users, so they should be accordingly distrusted. Tools such as WebProxy exist allow a user to edit and manipulate cookies on the fly.

+   Predictable session IDs make for an attractive target. In cases where persistent cookies are used, an attacker needs only to capture (or guess) the user’s session ID in order to be able to effectively hijack the user’s session.

+   All the state tracking methods are almost useless if not conducted consistently.

# Executing and Examining

+   Client-side scripting should not be relied on for sanitization. An attacker can easily subvert client-side scripting controls.

+   Basic authentication is a double-edged sword. Its encoding scheme means that unless coupled with SSL encryption, the requests are vulnerable to sniffing attacks. Tools also allow an attacker to brute force authentication protocols.

+   SSLv2 provides users the benefits of privacy gained by the use of encryption, but also allows an attacker a secure channel for attack.

+   SSLv3 requires careful thought before successful deployment. It offers client-side certificates, but developers must remember to change the default list of trusted certificate authorities that come preinstalled on most Web servers.

# Using Automation

+   Hidden/obscure directories can be found with spidering or brute force technologies found in tools such as Lynx or TelePort Pro.