+   3. Add the key and digital certificate to the web host.
a. Enter vi /etc/httpd/conf.d/ssl.conf to open the SSL configuration file.

+   b. Locate the line "SSLCertificateFile /etc/pki/tls/cert/localhost.crt."

+   c. Delete localhost.crt.

+   d. Switch to the insert mode.

+   e. Type server.crt to set the server.crt file as the default certificate file.

+   f. Press Esc to switch to the command mode.

+   g. Locate the line "SSLCertificateKeyFile /etc/pki/tls/private/localhost.key."

+   h. Delete private/localhost.key.

+   i. Switch to the insert mode.

+   j. Type certs/server.key to set the certs/ server.key file as the key file.

+   k. Press Esc to switch to the command mode.

+   l. Save and close the file.

+   4. Check whether the settings have been applied.
a. Enter clear to clear the terminal screen.

+   b. Restart the web service.

+   c. At the Enter pass phrase prompt, enter ourglobalcompany indicating that the certificate and key has been applied.

+   d. Observe that the web service is restarted only when the correct pass phrase is entered.

+   e. Clear the terminal screen.