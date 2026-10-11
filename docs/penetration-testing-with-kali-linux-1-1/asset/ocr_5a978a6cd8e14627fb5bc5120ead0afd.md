To view the certificate, we click CA Certificate on this screen (or connect to http://burp/cert) and save the cacert.der file to our local machine.

![](bbox=[0.13, 0.17, 0.87, 0.52])

Figure 112: Downloading the Burp Suite Certificate

Once the download is complete, we can drag and drop the downloaded file into Firefox, select Trust this CA to identify websites and click OK.

![](bbox=[0.22, 0.61, 0.78, 0.81])

Figure 113: Import the Certificate into Firefox

To verify the import was successful, we can again browse to a site using HTTPS, such as https://www.google.com, which should load without a warning and generate HTTPS traffic within BurpSuite's HTTP History tab.