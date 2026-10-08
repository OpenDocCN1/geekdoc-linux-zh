
# Hacking Exposed Web Applications

ones!) and automatically determines if you already have the correct version. However, we don't think this convenient site is justification for leaving ActiveX enabled all the time. Even more frustrating, when ActiveXScript is disabled under IE, the autosearch mechanism that leads the browser from a typed-in address like “mp3” to http://www.mp3.com does not work.

One solution to this problem is to manually enable ActiveX when visiting a site and then manually shut it off again. The smarter thing to do is to use the Trusted Sites security zone. Assign lower level of security (we recommend) to use this zone, and add trusted sites like WU (windowsupdate.microsoft.com) to it. Way, when visiting WU, the weaker security settings apply and the site's ActiveX features still work. Similarly allow search from the address bar. Aren't security zones convenient?

When configuring security zones, be sure to select which zone you want to apply content displayed in the main reader. We strongly recommend setting it to Restricted Sites (This is the default setting in Outlook 2000 for the security update patch, and later versions). Make sure that the Restricted Sites are configured to disable all active content! This sets it to High, and then use the Custom button to go back and manually disable everything that High leaves open (Or set them to high if disabling is not available). Figure 12-3 shows how to configure Outlook for Restricted Sites. So, to summarize our recommendations for IE Security Zones:

- Configure the Internet zone according to Table 12-1.
- Assign a setting of Medium to the Trusted Sites zone, and manually add sites to that zone you trust to run active content.
- Disable everything in the Restricted Sites zone.
- Configure Outlook Express to use the Restricted Sites to read e-mail.

Server-Side Countermeasures Based on the sample attacks we have demonstrated, server-side countermeasures for active content should be fairly obvious to Web developers. This advice is particularly relevant to ActiveX. If you are planning on implementing an ActiveX control to lend client-side functionality to your Web application, you should carefully consider the following:

- Don't mark the control “safe” at all; if you do mark it safe, ensure that it performs only the most benign functions and subject it to independent security review.
- Write/distribute controls, don't perform privileged actions (like launch files named setup.exe.).
- Be prepared to rapidly patch vulnerabilities as they are found (for example, Gator Corp. released a patch to Setup control, now available on Web site; see “References and Further Reading”).

## Chapter 12: Web Client Hacking

### CROSS-SITE SCRIPTING

Of equal impact to Web application are cross-site scripting vulnerabilities. We've shown an example using <SCRIPT>, <OBJECT>, <APPLET>, and <EMBED> tags can also work. When subsequent users browse the guestbook, their browsers will render the HTML, encounter the JavaScript by the first user, and execute the code. In this example, a JavaScript alert is sent, popping up a window with the text "Hello," as shown in Figure 12-4.

If this trick works, then you have a good chance of implementing a full cross-site scripting attack against the app. True to actually exploit cross-site scripting vulnerability, an attacker would need to set up a rogue server to capture the information input by victims of the injected script code. The server at 10.1.1.1 is the rogue server to capture the unsuspecting user input, and pass.cgi is a simple script to parse the information, extract useful data (that is, the password), and return a response to the user. Figure 12-5 shows what the password dialog box looks like in Internet Explorer 6.

The example we've used here is quite simple. Other attacks that could be launched via cross-site scripting mechanisms include cookie harvesting and more complex form-based information gathering. A couple of other nasty elements that get injected via cross-site scripting are the <META REFRESH> and <IFRAME> HTML tags. <META REFRESH> tags can be used to redirect a browser to another site, if someone can inject a <META REFRESH> tag into your Web site, you can easily zap subsequent users who view the injected code to any other Web site (the tag actually looks like: <META HTTP-EQUIV-Refresh CONTENT="0"> URL=http://evilserver.net/>). The <iframe> tag opens an HTML iframe that can be used to render other active content or others in a suspicious fashion.

Although not technically a cross-site scripting exploit, we'd also highlight the following URL to illustrate another approach to tricking users into going into one site when they think they're going to another:

```
http://bigbank.com/script.asp&account=123@evilserver.com
```

A quick glance at this URL may lead you to believe that it points to bigbank.com, but if you note the @ character near the end, you'll realize that everything to the left of the @ is ignored by the browser, which assumes that it's a username when actually following this link (per the http://user:password@sitename syntax used by many browsers).

Clearly, to exploit a cross-site scripting vulnerability, the end user must take some action, whether it be clicking on a malicious link or crossing a Web page that was injected by an earlier user. Nevertheless, even though the logic of cross-site scripting may seem convoluted, and the likelihood of successfully exploiting it may seem low, remember that high-profile Web sites like ebay and E*TRADE got caught with cross-site scripting vulnerabilities. At the very least, the PR fallout from exposures could be quite embarrassing for a large Web site.

# Cross-Site Scripting Countermeasures

Like previous countermeasure discussions in this chapter, we've divided our discussion into client- and server-side recommendations.

## Hacking Exposed Web Applications

### Client-Side Countermeasures

As we've recommended already in this chapter, disable Scripting in the browser. This prevents malicious site operators or crafty e-mails from easily harvesting information. Also be sure to disable both <META REFRESH> and <IFRAME> tags if your browser supports it.

> Some Nestscape browser versions support scripts embedded in HTML using & enclosures. For example, &alert('document.cookie'); will display the Web site, and there are no <SCRIPT> tags.

> CERT has a lengthy discussion of additional input that should be examined, as well as further discussion of additional steps to mitigate the risk of cross-site scripting, at http://www.cert.org/tech_tips/malicious_code_mitigation/.
