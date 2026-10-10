![](bbox=[0.17, 0.08, 0.65, 0.32])

This does not necessarily mean that you are encountering anything illegal, immoral, or fattening. Many sites opt to go with *self-signed* certificates, not because they are trying to pull a fast one on you, but because there may not be any reason to validate the true owner of the certificate and they do not want to pay the cost of getting a certificate validated. Some reasons for using a *self-signed* certificate include:

+   - **The Web site accepts no input** — In this case, you as the end user have nothing to worry about. There is no one trying to steal your information because you aren’t giving out any information. Most of the time this is done simply to secure the Web transmission from the server to you. The data in and of itself may not be sensitive, but, being a good netizen, the site has enabled you to secure the transmission to keep third parties from sniffing the traffic.
+   - **The Web site caters to a small clientele** — If you run a Web site that has a very limited set of customers, such as an Application Service Provider, you can simply inform your users that you have no certificate signer and that they can browse the certificate information and validate it with you over the phone or in person.
+   - **Testing** — It makes no sense to pay for an SSL certificate if you are just testing a new Web site or Web-based application. Use a *self-signed* certificate until you are ready to go live.

# Creating a Certificate Service Request

To create a third-party validated SSL certificate, you must first start with a Certificate Service Request (CSR). To create a CSR, do the following on your Web server:

```
# cd /etc/pki/tls/certs
# make certreq
/usr/bin/openssl
```