+   * Enter a location and click "Search Numbers".
+   * Choose a number and click "Add to Cart".
+   * Click the "Cart" in the upper right.
+   * Under "Connection or Application", select your connection (mine was previously created as "VoIP").
+   * Purchase the number using your free credits by clicking "Place Order".
+   * Click "Voice", "Outbound Voice Profiles" then "Add new profile".
+   * Provide the name of "outgoingvoice" and click "Create".
+   * Click "Outbound Voice Profiles" then the "Edit" icon next to "outgoingvoice".
+   * Select your connection (VoIP) and click "Add Connection/Apps to Profile".
+   * Click "Voice", "Sip Trunking", "SIP Connections" then "Outbound Options" to the right of the connection.
+   * Enter your new phone number in "Caller ID Override", then click "Save".

# Telnx Linphone Configuration

+   * Launch Linphone and click the "Home" button.
+   * Choose the Account Assistant.
+   * Choose "Use A SIP Account".
+   * Enter a "Username" of your login name provided by Telnx.
+   * Enter a "Display Name" of your telephone number, such as "2025551212".
+   * Enter the "SIP Domain" as "sip.telnx.com".
+   * Enter the "Password" of your login credential provided by Telnx.
+   * Change the "Transport" to "TLS". If this ever fails, try "UDP" or "TCP".

Your Linphone application can now make and receive calls without adding any funds. This is unique to Telnx. If you want to commit to Telnx as your VoIP provider, be sure to add $20 in new funds to your account in order to prevent termination of the trial. This provides enough credits ($40) to provide VoIP service for over three years, including a single number and usage.

Telnx does not offer native SMS forwarding to their web portal or another number. The only option is self-hosting a forwarder to an email address as we did with Twilio. If you have your own domain and a shared web host, create a text file titled telnx.php with the following content. Change "your@email.com" to the address where you want to receive notifications. Change "@yourdomain.com" to your actual domain name.

```
<?php
$to = "your@email.com";
$subject = "Text Message from {$_REQUEST['From']} to {$_REQUEST['To']}";
$message = "{$_REQUEST['Body']}";
$headers = "From: telnx@yourdomain.com ";
mail($to, $subject, $message, $headers);
```

Upload the file to your web host. Afterward, your specific URL may be similar to https://yourdomain.com/telnx.php. Within Telnx, conduct the following.

+   * Click "Messaging", "Programmable Messaging", then "Add New Profile".
+   * Provide a name of "sms" and select "Twiat API".
+   * In both "webhook" fields, enter the URL of the PHP file previously created.
+   * Click "Save".
+   * Click "Numbers" then "My Numbers" within the left menu.
+   * Within your number entry, select "sms" in the "Messaging profile" field.