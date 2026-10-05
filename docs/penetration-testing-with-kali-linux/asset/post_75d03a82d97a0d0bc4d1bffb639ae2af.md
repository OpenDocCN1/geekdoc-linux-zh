
# Penetration Testing with Kali Linux

![](img/336d6ea891e7464f18ad64426619ced4_316_0.png)

Figure 164: Mountain Vegetables Single Page Application

Figure 164 shows the website's landing page. The text on the site states that the website is currently under development. Scrolling through the page and hovering over buttons, we find a way to download a brochure.

![](img/336d6ea891e7464f18ad64426619ced4_316_1.png)

Figure 165: Download PDF Brochure

When we click CURRENT, Firefox opens the document in a new tab where we can download it.
To display the metadata of any supported file,79 we can use exiftool.80 Let's provide the arguments -a to display duplicated tags and -u to display unknown tags along with the filename brochure.pdf.

```
kali@kali:# cd Downloads
```

79 (Exiftool, 2022), https://exiftool.org/#$supported
80 (Exiftool, 2022), https://exiftool.org/

# OffSec Penetration Testing with Kali Linux

```
kalikali:~/Downloads$ exiftool -u brochure.pdf
Exiftool Version Number : 12.41
File Name : brochure.pdf
Directory : 
File Size : 303 KiB
File Modification Date/Time : 2022:04:27 02:37:04:00
File Access Date/Time : 2022:04:28 07:56:58:00
File Inode Date/Time : 2022:04:28 07:56:54:00
File Permissions : -rw-
File Type : PDF
File Type Extension : pdf
MIME Type : application/pdf
PDF Version : 1.7
Linearized : No
Page Count : 4
Language : en-US
Tagged PDF : Yes
XMP Tool : Image::ExifTool 12.41
Creator : Stanley Velantes
Title : Mountain Vegetables
Author : Stanley Stanley
Producer : Microsoft PowerPoint® for Microsoft 365
Create Date : 2022:04:27 07:34:01+02:00
Create Tool : Microsoft PowerPoint® for Microsoft 365
Modify Date : 2022:04:27 07:34:01+02:00
Document ID : uuid:B6EED371-D165-4BD4-B9C9-A15FA9C3A3CF
Instance ID : uuid:B6EED371-D165-4BD4-B9C9-A15FA9C3A3CF
Title : Mountain Vegetables
Author : Stanley Velantes
Create Date : 2022:04:27 07:34:01+02:00
Modify Date : 2022:04:27 07:34:01+02:00
Producer : Microsoft PowerPoint® for Microsoft 365
Creator : Stanley Velantes
```

Listing 2.1: Displaying the metadata for brochure.pdf

This generated list of the most important information include the file creation date, last modified date, the author, the operating system, and the application used to create the file. The Create Date and Modify Date reveal the relative age of the document. Given that these dates are recent (at the time of this writing) we have a high level of trust that this is a good source of metadata. The Author section reveals the name of the employee. We could use our knowledge to establish a trust relationship by dropping their name casually into a targeted email or conversation. This is especially helpful if the author maintains a relatively small profile. The output further reveals that the PDF was created with Microsoft PowerPoint for 365. This is crucial for us to plan our client-side attack since we know that the target uses Office and since there is no mention of "macOS" or "Mac" in any of the tags, it's probable that Windows was used to create this document. We can now leverage client-side attack against systems to create malicious documents.

## 11.1.2 Fingerprinting

In this section we will discuss Fingerprinting, also known as Device Fingerprinting, to obtain operating system and browser information from a target in a non-routable network. For example, we may be tasked with establishing an initial foothold on a target's network for a penetration test. Let's assume we previously extracted an email address with theHarvester. As a client-side attack we could use an HTML Application (HTA) to execute code in the context of Internet Explorer to some extent. This is a very popular attack to get an initial foothold in a target's network and is used by many threat actors. Before we do, we need to confirm that our target is either Internet Explorer or Microsoft Edge. We'll use Canarytokens, a free web service that generates a link with an embedded token that we will send to the target. When the target opens the link in the browser, we will get information about their browser, operating system. With this information we can confirm that the target is running Windows and should attempt an attack. Before we create our tracking link, we will discuss pretext like this. In a majority of situations, we can't just ask the stranger to click a link in an arbitrary way. Therefore, we should create pretext by leveraging the target's job role. For example, let's assume our target is working in the financial department. In this case, we may receive an invoice, but we offer a link that says a screenshot of the invoice with the error highlighted. This is of course the Canarytoken link. When the target clicks the link, it creates a fingerprint of the target providing us with the necessary information to prepare our client-side attack. The target will always receive a blank page when they click the link. With our pretext in place, we'll create our link in Canarytokens by loading the token generation page. Figure 166 shows the landing page for the site.

(Note: The footnotes provided in the OCR are:)
81 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Device_fingerprint
82 (Github, 2022), https://github.com/laries/theHarvester
83 (Microsoft, 2013), https://msdn.microsoft.com/en-us/library/ms53496(VS)
84 (The Hacker News, 2021), https://thehackernews.com/2021/04/lazar-apt-hackers-are-now-using.html
85 (Canarytokens, 2022), https://canarytokens.com
86 (Imperva, 2022), https://www.imperva.com/learn/application-security/pretexting/
87 (Canarytokens, 2022), https://canarytokens.org/generate

# Penetration Testing with Kali Linux

![](img/336d6ea891e7464f18ad64426619ced4_319_0.png)

Figure 166: Canarytokens Landing Page

The web form provides us with a dropdown menu to select the kind of tracking token we want to create. We must enter an email address to get alerts about the tracking token or provide a webhook URL. For this example, we'll select **Web bug URL** token from the dropdown menu, **https://example.com** as webhook URL, then enter **Fingerprinting** as the comment. After we enter this information, we'll click **Create my Canarytoken**.

![](img/336d6ea891e7464f18ad64426619ced4_319_1.png)

Figure 167: Enter example.com in web form

A new page with a blue window appears stating that our web token is now active:

# Penetration Testing with Kali Linux

![](img/336d6ea891e7464f18ad64426619ced4_320_0.png)

Your Web token is active!
Copy this URL to your clipboard and use as you wish:

```
http://canarytokens.com/tags/articles/static/7u2J
```

Remember, it gets triggered whenever someone requests the URL.
If the request is served as an image (<img src=""> then a 1x1 image is served.
The URL is viewed in a browser then a blank page is served with fingerprinting Javascript.

Ideas for use:

- In an email with a juicy subject line.
- Embedded in documents.
- Inserted into canary webpages that are only found through brute-force.
- This is just an example. Apart from the hostname and the actual token (random string), you can change all other parts of the URL.

Figure 16: Active Canarytoken

This page contains the tracking link we can use to fingerprint targets. It also provides ideas on how to get a target to click the link.

Next, let's click on Manage this token, which is located on the upper-right corner of the page. This will bring us to the token settings.

New token History

![](img/336d6ea891e7464f18ad64426619ced4_320_1.png)

# Token settings

| Webhook reporting | ON |
| --- | --- |
| Browser scanner | ON |

Here's your Web token:

```
http://canarytokens.com/tags/articles/7u2J
```

This token has not been triggered yet

We hope you are enjoying the free version of Canarytokens!
For (non-public) tokens, support, mass-deployment-tools and better management of your deployed tokens, check out our commercial Canarytokens offering at https://canarytokens.com/canarytokens.
