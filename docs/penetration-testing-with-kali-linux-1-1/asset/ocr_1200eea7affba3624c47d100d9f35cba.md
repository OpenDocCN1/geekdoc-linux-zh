![](bbox=[0.11, 0.04, 0.28, 0.09])

Even though each Burp Suite CA certificate should be unique, we will ensure this by regenerating it. To do this, we will navigate to **Proxy > Options > Proxy Listeners** in BurpSuite and click **Regenerate CA certificate** as shown below:

![](bbox=[0.14, 0.18, 0.87, 0.56])

*Figure 110: Regenerating Burp’s CA Certificate*

Click **Yes** on the confirmation dialog and restart Burp Suite.

To import the new CA certificate into Firefox, we will first browse to **http://burp** to find a link to the certificate:

![](bbox=[0.14, 0.67, 0.87, 0.8])

*Figure 111: Burp Welcome Page*