# # OffSec Penetration Testing with Kali Linux

Burp Project Intruder Repeater Window Help
Dashboard Target Repeater Options Sequencer Decoder Extender Project options User options Learn
Intercept HTTP History WebSockets History

Filter: Hiding image and general binary content

| B | Host | Method | URL | Parameters | Edit | Status | Length | Mime type | Extension | Title |
|---|---|---|---|---|---|---|---|---|---||
| 1 | http://offsec | GET | /login.php | | | 200 | 607 | HTML | | Log in & logic: OffSec: R |
| 2 | http://offsec | GET | /wp-admin/images/wp-login-logo.png | | | 200 | 1774 | PNG | Log in & logic: OffSec: R |
| 3 | http://offsec | POST | /login.php | | | 200 | | HTML | |

Request

![](bbox=[0.118, 0.315, 0.882, 0.535])

Figure 96. Sending the POST request to Intruder

We can now select the Intruder tab in the upper bar, choose the POST request we want to modify, and move to the Positions sub-tab. Since the user admin is correct, we only need to brute force the password. First, we press Clear to make sure all fields are cleared. We can then select the value of the keyword and press the Add button on the right.

Burp Project Intruder Repeater Window Help
Dashboard Target Repeater Options Sequencer Decoder Extender Project options User options Learn

Payloads

![](bbox=[0.118, 0.695, 0.882, 0.815])

Figure 97. Assigning the password to the Intruder generator

PWK - ©2023 OffSec Services Limited. All rights reserved.