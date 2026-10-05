
# Penetration Testing with Kali Linux

Figure 169: Management of Canarytoken

The token has not been triggered, but this is to be expected since we just created it. For this example, we will keep the default settings, since we are simply fingerprinting the target and not embedding the token in a web application or web page.

Next, let's click on History in the upper right corner. The History page shows us all visitors clicked our Canarytoken link and the information about the victim's system. As of now the list is empty.

![](img/336d6ea891e7464f18ad64426619ced4_321_0.png)

| History for Canarytoken: |
| :--- |
| 7u303y650trp489lifwrpszl |
| Heads Up! Click the items for more info. |
| Incident List is Currently Empty |

Brought to you by Theical Canary, our easy-to-use honest solution that deploys in just four minutes. Know. Which matters.
© Theical Canary 2015-202

Figure 170: Canarytoken History

Let's assume we have convinced our victim, in the context of our pretext, to visit the Canarytoken link via email. As we convinced the victim clicks our link, they get a blank page in their browser. At the same time, a new entry appears in our history list:

| History for Canarytoken: |
| :--- |
| 7u303y650trp489lifwrpszl |
| Heads Up! Click the items for more info. |
| Incident Map | Incident List |
| Date: 2022 Apr 25 17:47:01.23963 (UTC) IP: 38.146.5.222 Channel: HTTP |

Figure 171: Canarytoken with Entry

A map on the left side shows us the geographical location of the victim. We can click on the entry to get more information.

# OffSec

Penetration Testing with Kali Linux

![](img/336d6ea891e7464f18ad64426619ced4_322_0.png)

Figure 172: Detailed Information of Canarytoken Entry

The upper-half of the detailed view provides information about the victim's location and attempts to determine the organization name. The user agent sent by the victim's browser is also displayed. From the user agent itself we can infer the target's operating system and browser. However, the user agent can be modified and is not always a reliable source of information.

In this example, the victim's user agent implies they use the Chrome browser on a 64-bit Windows 10 system. We could also use an online user agent parser,⁴⁸⁸⁸ which interprets the user agent for us and offers us a more user-friendly result.

Let's scroll down to the Browser area.

> ⁴⁸⁸⁸ (WhatMyBrowser, 2022), https://developers.whatismymbrowser.com/useragents/parse/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved. 323

# OffSec

Penetration Testing with Kali Linux

## Browser

| | |
|---|---|
| mimetypes | Portable Document Format;pdf,application/pdf\|Portable Document Format;pdf,text/pdf\| |
| vendor | Google Inc. |
| language | en-US |
| enabled | True |
| installed | True |
| platform | Win32 |
| version | 101.0.4951.41 |
| os | Windows |
| browser | Chrome |

Figure 173: Detailed Browser Information

Figure 13 shows additional information about the victim’s browser. This information does not come from the user agent, but from JavaScript fingerprinting code embedded in the Canarytoken web page. This information is more precise and reliable than the information from the user agent. This again suggests that the target is running Chrome on Windows.

The Canarytoken service also offers other fingerprinting techniques. Let’s navigate back to the Canarytokens menu to discuss these.

![](img/336d6ea891e7464f18ad64426619ced4_323_0.png)

Figure 174: Other Methods

The dropdown menu provides options to embed a Canarytoken in a Word document or PDF file, which would provide us information when victim opens the file. Furthermore, we could also embed it into an image, which would inform us when it is viewed.

PWK - © 2023 OffSec Limited. All rights reserved. 324

# OffSec

Penetration Testing with Kali Linux

We could also use an online logger Grabify⁴⁸⁹ or JavaScript fingerprinting libraries such as fingerprint.js⁹⁰ In this section, we demonstrated an effective fingerprinting technique that revealed critical information about our target's system. While our goal was to determine if the target runs Windows and Internet Explorer or Microsoft Edge enabled, we could only identify victim runs Chrome. In a situation like this, we should either use a different client-side attack vector or change our pretext to, for example, suggest that the screenshot is viewable in Internet Explorer or Microsoft Edge.

This Learning Unit covers the following Objectives:

- Understand variations of Microsoft Office client-side attacks
- Install Microsoft Office
- Leverage Word Macros

Ransomware attacks have increased dramatically in recent years⁹¹ In cases, the initial breach involved a malicious macro. This is a common attack vector since ubiquitous documents are commonly emailed by colleagues.

In this Learning Unit, we'll first discuss various considerations of malicious documents in a client-side attack scenario. Next we'll walk through the installation process and finally, we'll create a malicious document with embedded macros to obtain a reverse shell.

### 1.2. Preparing the Attack

Before we jump into the hands-on elements of this Learning Unit, let's discuss three important considerations when we use malicious documents in client-side attack.

First, we must consider the delivery method of our document. Since malicious macro attacks are well-known, email providers and spam filter often filter out all Office documents by default. Therefore, in majority of situations we can't just send the malicious document as an attachment. Furthermore, most anti-phishing programs stress the danger of enabling macros in an emailed document.

To deliver our payload and increase the chances that the target opens the document, we could use a pretext and provide the document in another way, like a download link. If we successfully manage to deliver the document to our target via email or download link, the file will be tagged with Mark of the Web (MOTW)⁹² and open in Protected View.⁴³

⁴⁸⁹ (Grabify, 2022), https://grabify.com/link/
⁹⁰ (Github, 2022), https://github.com/fingerprints
⁹¹ (Compartech, 2022), https://www.compartech.com/antivirus/ransomware-statistics/
⁹² (MITRE ATT&CK, 2022), https://attack.mitre.org/techniques/T1553/005/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved. 325

which disables all editing and modification settings in the document and blocks the execution of macros or embedded objects. When the victim opens the MOTW-tagged document, Office will show a warning with the option to *Enable Editing*.

| File Home Insert Draw Layout References Review Mailing View Search (Alt+Q) |
| **PROTECTED VIEW** Be careful—files from the internet can contain viruses. You need to edit them; it's safer to save in Protected View. | Enable Editing |

Figure 15: Protected view in action

We could also use other macro-enabled Microsoft Office programs that lock Protected View, like Microsoft Publisher, but this is less frequently asked.

Finally, we must consider Microsoft's announcement that discusses blocking macros by default.⁴⁴ This change affects Access, Excel, PowerPoint, Visio, and Word. Microsoft implemented this in majority of Office versions such as Office 2021 all the way back to Office 2013. The implementation dates for various channels are in the corresponding Microsoft page.⁴⁵

The announcement states that macros in files delivered via the internet may no longer be activated by the click of a button, but by following a more tedious process. For example, when a user opens a document with embedded macros, they will no longer receive the *Enable Content* message:

![](img/336d6ea891e7464f18ad64426619ced4_325_0.png)

Figure 16: Possibly to execute macros by clicking one Button

Instead, they will receive a new, more ominous message with a *Learn More* button:

![](img/336d6ea891e7464f18ad64426619ced4_325_1.png)

If users click on *Learn More*, the resulting Microsoft web page⁴⁶ outlines the dangers of enabling macros.

Additionally, Microsoft provides instructions on how to unlock the macro by checking *Unblock* under file properties.

⁴⁹³ (Microsoft, 2019), https://support.office.com/en-us/article/what-is-protected-view-d6f09ac7-e6b9-4ea3-84bbcdbc6653
⁴⁹⁴ (TechCommunity, 2022), https://techcommunity.microsoft.com/t5-microsoft-365-blocking/helping-users-stay-safe-internet-macros-by-default/pd-307185
⁴⁹⁵ (Microsoft Learn, 2023), https://learn.microsoft.com/en-us/deployoffice/security/internet-blocked
⁴⁹⁶ (Microsoft Support, 2022), https://support.microsoft.com/en-us/topic/a-potentially-dangerous-macro-has-been-blocked
