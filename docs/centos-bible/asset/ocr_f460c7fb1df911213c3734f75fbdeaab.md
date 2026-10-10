# FIGURE 13-3

A Page window alerts you when a site is not authenticated.

![](bbox=[0.13, 0.18, 0.82, 0.55])

This does not necessarily mean that you are encountering anything illegal, immoral, or flattering. Many sites opt to go with self-signed certificates, not because they are trying to pull a fast one on you, but because there may not be any reason to validate the true owner of the certificate and they do not want to pay the cost of getting a certificate validated. Some reasons for using a self-signed certificate include:

+   -   **The Web Site Accepts No Input** — In this case, you as the end-user have nothing to worry about. There is no one trying to steal your information because you aren't giving out any information. Most of the time this is done simply to secure the Web transmission from the server to you. The data in and of itself may not be sensitive, but, being a good *citizen*, the site has enabled you to secure the transmission to keep third parties from sniffing the traffic.
+   
+   -   **The Web Site Caters to a Small Clientele** — If you run a web site that has a very limited set of customers, such as an Application Service Provider, you can simply inform your users that you have no certificate signer and that they can browse the certificate information and validate it with you over the phone or in person.
+   
+   -   **Testing** — It makes no sense to pay for an SSL certificate if you are just testing a new web site or Web-based application. Use a self-signed certificate until you are ready to go live.