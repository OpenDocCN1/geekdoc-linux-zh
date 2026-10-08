Follow these steps to create your own certificate.

+   1. Change to the directory where the certificate generating makefile is located:

```
cd /usr/share/ssl/certs
```

+   2. Make the new certificate by entering this command:

```
make testcert
```

+   3. You're prompted for the pass phrase you created in the preceding section. Enter the pass phrase when you're prompted.

You're prompted to enter information about your location, IP address, and other information that can help identify your certificate as valid. These steps outline the questions and what you need to enter.

+   4. You're prompted to enter your country code.

For example, enter US if you live in the United States, GB for Great Britain, or MX for Mexico.

+   5. Enter your state (for the United States) or province name. (Don't abbreviate the name.)

For example, enter New Mexico.

+   6. Enter your city name.

In this example, enter Albuquerque.

+   7. Enter your organization or company name if you have one.

For example, enter Paunchy Heavy Industries, Ltd.

+   8. Optionally, enter your suborganization, if you have one.

+   9. Enter the full name of your web server.

For example, the sample web server is named Veracruz, and the network name is paunchy.net. Therefore, you enter veracruz.paunchy.net.

The name of your server must match its DNS name (if you run your own DNS server). If the two don't match, you're prompted to access or reject the certificate every time you connect to the web server.

+   10. Enter your e-mail address:

```
paul@paunchy.net
```

Your certificate is constructed. Restart your web server with this command:

```
/etc/init.d/httpd restart
```