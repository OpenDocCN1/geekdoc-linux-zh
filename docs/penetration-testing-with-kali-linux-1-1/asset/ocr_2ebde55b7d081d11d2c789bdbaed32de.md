Official website: **http://beefproject.com/**

# ## Getting Started

Welcome to BeEF!

Before being able to fully explore the framework you will have to ‘hook’ a browser. To begin with you can point a browser towards the basic demo page **here**, or the advanced version here.

If you want to hook ANY page (for debugging reasons of course), drag the following bookmarklet link into your browser’s bookmark bar, then simply click the shortcut on another page: Hook Me!

After a browser is hooked into the framework they will appear in the ‘Hooked Browsers’ panel on the left. Hooked browsers will appear in either an online or offline state, depending on how recently they have polled the framework.

# ## Hooked Browsers

To interact with a hooked browser simply left-click it, a new tab will appear. Each hooked browser tab has a number of sub-tabs, described below:

+   1.  **Main:** Display information about the hooked browser after you’ve run some command modules.
+   2.  **Logs:** Displays recent log entries related to this particular hooked browser.
+   3.  **Commands:** This tab is where modules can be executed against the hooked browser. This is where most of the BeEF functionality resides. Most command modules consist of Javascript code that is executed against the selected Hooked Browser. Command modules are able to perform any actions that can be achieved through Javascript; for example they may gather information about the Hooked Browser, manipulate the DOM or perform other activities such as exploiting vulnerabilities within the local network of the Hooked Browser.

Each command module has a traffic light icon, which is used to indicate the following:

+   -   🟢 The command module works against the target and should be invisible to the user
+   -   🟠 The command module works against the target, but may be visible to the user
+   -   ⚪ The command module is yet to be verified against this target
+   -   🔴 The command module does not work against this target

+   4.  **XssRays:** The XssRays tab allows the user to check if links, forms and URI path of the page (where the browser is hooked) is vulnerable to XSS.
+   5.  **Rider:** The Rider tab allows you to submit arbitrary HTTP requests on behalf of the hooked browser. Each request sent by the Rider is recorded in the History panel. Click a history item to view the HTTP headers and HTML source of the HTTP response.
+   6.  **Network:** The Network tab allows you to interact with hosts on the local network(s) of the hooked

![](bbox=[0.18, 0.11, 0.85, 0.76])

Figure 259. Accessing the demo page on BeEF

Once our browser is hooked, it will appear in the “Hooked Browsers” panel of the BeEF console as the localhost IP 127.0.0.1. Clicking our IP (now known as a zombie) should present us with a new page containing details about our victim browser. We can then proceed to the Commands tab under which we can find various enumeration scripts and exploits: