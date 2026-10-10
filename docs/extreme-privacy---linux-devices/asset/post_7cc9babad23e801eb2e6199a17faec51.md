
Click "Voice", "Settings", and "General" in the left menu.
- Disable "Request Inspector" and click "Save".

All of this logging may seem invasive. It is, but it is not unique to Twilio. Twilio is doing nothing more than every other telephony provider including cellular and landline telephone companies. We have some control of how the data is stored, but I do not want to present false expectations here. While Twilio may appear to have deleted your call logs, voicemails, messages, and transcriptions, they are all likely still stored somewhere within their system. Our only goal is to remove the data from within our dashboard. Never expect any level of privacy when it comes to traditional phone calls and messages. VoIP services should never be used for sensitive communication. Assume there is a log of everything which will be stored forever.

## Telnx VoIP Service

In past writings, I highly recommended a Twilio alternative called Telnx. At the time, they were less scrupulous of new accounts and encouraged people to try their services. Today, I urge caution before proceeding. This is due to several issues.

- Telnx only provides accounts to confirmed businesses. However, your new custom domain email address may suffice.
- Telnx no longer provides actual customer support. Support tickets only receive canned responses, and the request is eventually closed without a solution. Calls to their support line inform you to send an email, which is never answered. You will need to do your own troubleshooting if required.
- Telnx does not provide voicemail services.
- Telnx does not allow you to delete your user logs or text messages from their system in the way Twilio does.
- Telnx suspends paid accounts if their automated fraud system detects unusual activity. I have experienced this myself when an unused account appeared suspicious to them. When I questioned about this practice, I was ignored.

However, I know of some people who prefer Telnx over Twilio. Their monthly number fee is slightly less and redundancy is always a good thing. If the Twilio tutorial did not generate the usage you desire, possibly due to a suspended account, you might consider Telnx (https://refer.telnx.com/refer/zrfmo). This VoIP provider replicates the service provided by Twilio, but their setup process is easier. Now that you have an understanding of Twilio, I will abbreviate the steps here for Telnx.

- Create a free account at https://refer.telnx.com/refer/zrfmo . This specific URL provides $20 in free credits which can be used right away.
- Provide a custom domain email address, which was previously explained.
- If prompted for purpose, choose "SIP Trunking".

You should now be logged in to the Telnx portal. You can now create your first connection and purchase a telephone number.

- Click "Voice" then "SIP Trunking" from the side menu.
- Click the "+ Add SIP Connection" button.
- Enter the name you wish to have for your connection (I chose "VoIP").
- Click "Create Sip Connection".
- Enable "Credentials" as the "Connection Type".
- Copy the username and password automatically generated.
- Click "Save and finish editing".
- Click "Numbers", "My Numbers", and "Search & Buy Numbers".
- Enter a location and click "Search Numbers".
- Choose a number and click "Add to Cart".
- Click the "Cart" in the upper right.
- Under "Connection or Application", select your connection (mine was previously created as "VoIP").
- Purchase the number using your free credits by clicking "Place Order".
- Click "Voice", "Outbound Voice Profiles" then "Add new profile".
- Provide the name of "outgoingvoice" and click "Create".
- Click "Outbound Voice Profiles" then the "Edit" icon next to "outgoingvoice".
- Select your connection (VoIP) and click "Add Connection/Apps to Profile".
- Click "Voice", "Sip Trunking", "SIP Connections" then "Outbound Options" to the right of the connection.
- Enter your new phone number in "Caller ID Override", then click "Save".

## Telnx Linphone Configuration

- Launch Linphone and click the "Home" button.
- Choose the Account Assistant.
- Choose "Use A SIP Account".
- Enter a "Username" of your login name provided by Telnx.
- Enter a "Display Name" of your telephone number, such as "2025551212".
- Enter the "SIP Domain" as "sip.telnx.com".
- Enter the "Password" of your login credential provided by Telnx.
- Change the "Transport" to "TLS". If this ever fails, try "UDP" or "TCP".

Your Linphone application can now make and receive calls without adding any funds. This is unique to Telnx. If you want to commit to Telnx as your VoIP provider, be sure to add $20 in new funds to your account in order to prevent termination of the trial. This provides enough credits ($40) to provide VoIP service for over three years, including a single number and usage.

Telnx does not offer native SMS forwarding to their web portal or another number. The only option is self-hosting a forwarder to an email address as we did with Twilio. If you have your own domain and a shared web host, create a text file titled telnx.php with the following content. Change "your@email.com" to the address where you want to receive notifications. Change "@yourdomain.com" to your actual domain name.

```php
<?php
$to = "your@email.com";
$subject = "Text Message from {$_REQUEST['From']} to {$_REQUEST['To']}";
$message = "{$_REQUEST['Body']}";
$headers = "From: telnx@yourdomain.com ";
mail($to, $subject, $message, $headers);
```

Upload the file to your web host. Afterward, your specific URL may be similar to https://yourdomain.com/telnx.php. Within Telnx, conduct the following.

- Click "Messaging", "Programmable Messaging", then "Add New Profile".
- Provide a name of "sms" and select "Twilio API".
- In both "webhook" fields, enter the URL of the PHP file previously created.
- Click "Save".
- Click "Numbers" then "My Numbers" within the left menu.
- Within your number entry, select "sms" in the "Messaging profile" field.
- Confirm the rate notice if prompted.

Incoming text messages should now be forwarded to your email address. The subject will identify the sender and recipient while the message body will display the text message. This method prevents Telnx from storing all of your incoming messages (content) on their own server in the way that Twilio does, but they still maintain a permanent log. They would still have the ability to intercept and see the contents, but that is unlikely. Once the message is routed to your email, you should be the only host of the content (but not the log).

If you want to send a text from your new Telnx number, click "Messaging" > "Programmable Messaging" > "Learn & Build" > "Send & Receive a Message". You can use the online form to send a SMS text message to any number. You can also use the commands provided on that page to send messages from within Terminal. Similar to Twilio, I do not use this feature. I never use a VoIP number for back-and-forth conversations. I only need to receive the occasional confirmation text message, which forwards to my email from both providers.

You can customize the caller ID name displayed during your outgoing calls within the Telnx portal. Click "Numbers" | "My Numbers" from the menu and then "Caller ID/CNAM Listing" under the services area of your chosen number. Enable the "CNAM Listing" and "Caller ID Name" options, then enter any name desired. It may take a week to take effect. Be sure to enable two-factor authentication (2FA) through "My Account" in the "Security" section.

While this configuration is simpler than Twilio, it has less features. However, there are also benefits which are not available with Twilio. Consider the following.

- With Twilio, unanswered calls went directly to voicemail, and messages were transcribed and emailed to me. With Telnx, unanswered calls disconnect after about 30 seconds. There is a voicemail option, but it requires a paid third-party service. If you want voicemail and transcription, Twilio is best.
- Twilio allows incoming text messages to be natively delivered directly to your dashboard or forwarded to any other number. Telnx requires you to host your own message forwarding server for this to work. If you need the number to support incoming SMS text without third-party services, then Twilio is the appropriate option. If you have your own website, replicating this is fairly easy.
- Twilio possesses numerous fraud triggers which can impact our usage. Many readers report difficulties simply creating an account and being allowed access. Telnx provides immediate access upon registration of a "business" email address. However, I have witnessed Telnx suspend accounts created using free email domains behind a VPN. Always provide an email address associated with a custom domain while connected to public Wi-Fi in order to present the highest chance of obtaining a new account. Since you will be using this service to make and receive telephone calls associated with your real name, I see very little reason to attempt registration with an alias.
- The pricing and overall call quality for Telnx and Twilio is almost identical.

I currently maintain numbers through both services and configure each into Linphone. If I were forced to rely on only one service, it would be Twilio due to the voicemail recording, sanitization options, and overall stability. If you have a Telnx account and it works for you, great. However, I encourage others to focus their efforts on Twilio. I currently maintain several numbers through Twilio and configure each into Linphone. Incoming SMS text messages are forwarded to my email account via my website.
