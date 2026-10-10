
- If prompted, choose "Use a SIP Account". If this is not present, click the "Home" button and choose "Account Assistant".
- If prompted, click "I understand" about any restrictions.
- Enter a "Username" of your number, such as "2025551212".
- Enter a "Display Name" for your telephone number, such as "2025551212".
- Enter the appropriate "SIP Domain", such as 2025551212.sip.us1.twilio.com.
- Enter the "Password" you previously created for the credential account.
- Change the "Transport" to "TLS". If this ever fails, try "UDP" or "TCP".

Click the confirmations until you return to the main application. You can now click the number selection area in the upper left corner in order to select your new account, or choose between multiple accounts if you add more. You should see a green or grey light next to the account if the connection from Linphone to Twilio is successful. We can now make our first call.

- Confirm that your Twilio account is selected within the Linphone application.
- In the search field at the top, input any known telephone number.
- Click the "phone" button to initiate a call.

You should receive an automated message thanking you for using your demo account. I had to click the three dots, then the "Multimedia parameters" in order to select the appropriate incoming and outgoing sound properties. This confirms that we can place calls to Twilio's servers, but we are far from unlimited usage to real numbers. As long as you receive a confirmed test call message from Twilio, your configuration is complete. If you would like to remove all restrictions to make and receive calls to and from any number, you must "Upgrade" the account. The following should be conducted within the Twilio portal.

- Return to the Dashboard in the upper left menu.
- Click the "upgrade" link and provide all requested billing details.
- Provide any credit, debit, or registered prepaid card.
- Apply $20 to the account.

You should now have an unrestricted Twilio account which should be fully functional for voice calls. Please do not upgrade the account until you know your test calls are going through. You should also have a fully functional VoIP application which can facilitate calls. Linphone can be used to place a call at any time from your Linux device. You can also add as many numbers as you wish by repeating this process. Incoming calls will "ring" your Linux device as long as the Linphone application is open and your status is "green". Before you create dozens of new numbers, let's discuss the costs. Each Twilio number withdraws $1.15 every month from your balance. If you followed these steps, you are funded for almost three years of usage of the initial phone number. Incoming and outgoing calls cost $0.004 per minute. During all of my testing for this tutorial so far, I spent $1.21. There are several huge benefits with this strategy, as outlined below.

- You can now make and receive telephone calls through your Linux device.
    - Windows, Linux, Android, and iOS are also supported through Linphone.
- You have more control over your number(s). You are not at the mercy of Google, and their data collection, in order to process calls.
- You can add as many numbers as desired as long as you have the funds to support them. I have five numbers through Twilio and I can access all of them through every device I own. My annual cost for this, including my usage, is about $70. Twilio does not know my real name and only possesses a custom domain email address and Google Voice number in association to my account.
- You can port a number into Twilio. If you plan to cancel a cell phone or VoIP number, you can port it into Twilio and still have access through Linphone.
- This process works well with custom Android operating systems, such as GrapheneOS, as explained in the *Extreme Privacy: Mobile Devices* guide.
- You can call international numbers (at increased costs). Most VoIP providers such as Google, Twilio, and others restrict calling to nearby countries. You can enable any country in Twilio by navigating to Programmable Voice > Calls > Geo Permissions.

Please think of this VoIP strategy as being similar to landline service. While configuring Twilio within the Linphone application during testing of this strategy, I encountered several devices which presented authentication errors during usage. These usually claim that the Twilio credentials supplied to Linphone have failed and the user is prompted to enter the correct password. Supplying the appropriate password fails. This appears to be an issue with Twilio temporarily blocking access due to too many invalid attempts, incorrect protocol settings, or launching and closing of Linphone from mobile devices too many times within a sixty-minute threshold. Any account restrictions should reset after twenty minutes of inactivity, but the following settings within Linphone should mitigate these issues. Navigate to Preferences > Settings > SIP Accounts > Proxy Accounts and click the pencil icon (Edit) and confirm the following.

- Transport: TLS
- Register: Enabled
- Publish presence information: Enabled
- ICE/AVPF/STUN/TURN: Disabled
- Outbound Proxy: Disabled

Linphone software accepts multiple numbers for incoming and outgoing calls. However, their menu only allows you to place outgoing calls from the most recently added (default) number. You can select the default number for outgoing calls within the upper left number selection menu.

It is important to note that VoIP telephone calls and messages are not encrypted and we should expect no privacy. However, I have some isolation from my true identity. I use these numbers mostly for outgoing calls, such as calls to businesses. This strategy is an affordable option which allows telephone calls without relying on your cellular carrier-provided number. It can also be used to isolate outgoing "junk" calls which are likely to abuse your number. Twilio has the ability to see our logs, but so would any cellular carrier if we had made the calls via our official number. In a moment we will purge those logs as often as desired.

The biggest feature of this process is the ability to possess affordable VoIP numbers without a third-party service. Any time you allow a third-party service to facilitate your calls, you are also allowing them to intercept and see your data. All of these services rely on a VoIP provider such as Twilio, so I believe we should consider creating our own solutions and eliminate any additional companies which are unnecessary.

VoIP solutions often have limitations over traditional cellular communications. Twilio, and any services which rely on Twilio, do not always support "short codes". These are abbreviated phone numbers that are usually 5 or 6 digits in length. They are commonly used to send SMS and MMS messages with verification codes for account access. I think of these numbers as landline replacements which allow me to send and receive voice calls and personal texts. I maintain a single Google Voice account which can receive short codes. I explain more about this later.

By default, there is no name associated with the caller ID when you place a call from your Twilio number(s). This may be desired by some, but could be a disinformation campaign for others. On one of my Twilio numbers which I use for personal calls in my true identity, I attached my name to the caller ID. This way, my name appears as the caller on the screen of my bank or credit card company when I call from a Twilio number. It adds an extra layer of assurance. On another number, which I use with my alias name, I prefer that name to display as the caller. This also adds credibility to my call as an alias. Twilio requires you to contact their support in order to request these modifications.

Overall, I view this method as a simple and affordable phone line which provides unlimited numbers at my disposal. I can place calls from my laptop or mobile devices when needed without exposing my true cellular number. I can accept incoming calls on my laptop as if it was a traditional landline telephone. The person on the other end does not know I am using VoIP instead of a standard phone line. In my experience, VoIP calls while possessing a stable internet connection can be much more reliable than cellular calls with a weak signal.

# Twilio SMS Messaging

Linphone has no embedded voicemail or SMS/MMS text message capabilities and is only for voice calls. If you desire the ability to send SMS/MMS text messages associated with this new Twilio number, you must create an environment which can facilitate this communication. You have a few options for this, but I will present my recommended approach. The following allows you to forward any incoming SMS text messages to another telephone number, such as Google Voice or any other number. This is the simplest option for text message forwarding.

- Click the "TwiML Bins" option in the left menu then "My TwiML Bins".
- Click the plus to add a new bin and provide a name of "incomingsms".
- Insert the following within the TwiML field, replacing "12125551212" with your own receiving number, and click "Save".
  ```xml
  <Response><Message to="+12125551212">{{From}}:
  {{Body}}</Message></Response>
  ```
- Click "Phone Numbers", "Manage", "Active Numbers", then select number.
- Under "Messaging", and "A Message Comes In", choose "TwiML Bin".
- Choose "incomingsms" in the field to the right and click "Save".

All incoming text messages should now forward to your other number. Note that you pay a small fee for both the incoming and the forwarding text from your Twilio balance. Advanced users may want to instantly forward any incoming SMS text messages to an email address. **This requires an online web server and the knowledge of uploading files to it.** A shared host and any custom domain will suffice. Create a text file called twilio.php with the following content. Change "your@email.com" to the address where you want to receive notifications. Change "@yourdomain.com" to your actual domain name. Upload this file to your web host.

```php
<?php
$to = "your@email.com";
```
