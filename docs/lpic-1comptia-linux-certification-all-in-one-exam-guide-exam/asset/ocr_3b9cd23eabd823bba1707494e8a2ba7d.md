![](bbox=[0.16, 0.07, 0.32, 0.11])

![](bbox=[0.33, 0.06, 0.96, 0.4])

Let’s look at an example to see how public key cryptography works. Suppose you’re using a web browser to visit www.mydomain.com and you’ve found some product that you just can’t live without. You’ve put it in your shopping cart and are in the process of checking out from the online store. The process shown in Figure 18-3 occurs as you submit your credit card information to the e-commerce web server.

+   1.  Your browser requests the public key for www.mydomain.com from the external CA.
+   2.  The CA returns the public key to the browser, which then uses that key to encrypt the message.
+   3.  The browser sends the encrypted message to www.mydomain.com.
+   4.  The web server at the other end then uses its private key to decrypt the transmission.

![](bbox=[0.16, 0.69, 0.33, 0.75])

![](bbox=[0.33, 0.68, 0.96, 0.98])