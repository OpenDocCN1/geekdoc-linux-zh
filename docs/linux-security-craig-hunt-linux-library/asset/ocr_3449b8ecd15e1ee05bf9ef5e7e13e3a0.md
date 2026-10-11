# 7
# HTTP Services

This chapter continues the discussion of Part 3, “Application Security,” by taking an in-depth look at the Apache HTTP server, the dominant force behind the Web server explosion of the last five years. This chapter describes the overall security features of the base Apache package, as well as the standard authentication and access control configuration.

While system and network layer security can contribute to sealing most of the low-level threats to your Linux server, the harsh reality is that a service like HTTP requires you to open up a number of ports (TCP 80 and sometimes TCP 443) to the Internet population at large. This forces you to implement a complete set of security measures at the application layer, including authentication, access control, and the protection of the HTTP application server itself.

In addition, if your company conducts electronic commerce using your HTTP server, you’ll need to ensure the privacy of the transactions, as well as provide strong authentication to your prospective customers and business partners. This can be addressed using SSL (Secure Sockets Layer) extensions to the base Apache HTTP distribution. This chapter describes two different packages that you can deploy to ensure the privacy and authentication of your HTTP transactions:

+   - mod_ssl (part of the OpenSSL initiative)
+   - Apache-SSL, on which mod_ssl was originally based

Let’s kick off the discussion by describing the security-specific issues at play when you install, configure, and maintain the Apache HTTP server.