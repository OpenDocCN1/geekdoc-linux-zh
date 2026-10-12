# ### 25.3 Web URL filtering

Filtering on Web URLs is related to the content scanning we discussed in the previous module, but it works entirely differently. It controls access to Web pages on the basis of the URL string only, not by inspecting the content of the page the URL points to.

You configure your desktop HTTP clients to use the URL filter as their HTTP proxy. When a client requests a page, the filter system in the proxy looks up the URL in an internal database containing a huge number of URLs and their classifications, to find out what type of Web page the user requested (e.g. pages on **www.playboy.com** contain nudity and information on recreational drugs). If the administrator has forbidden this type of page, the user's request is blocked (shown at 2a in Figure 25.3), otherwise the request is honored (shown at 2b). The system doesn't even need to connect to the remote Web server because it's not checking the content of the page, merely its URL. To ensure nobody bypasses the filter, block all HTTP traffic (except to/from the filter machine) at your firewall.

![](bbox=[0.18, 0.33, 0.72, 0.61])

**Figure 25.3** Request is either blocked or permitted, depending on classification of the URL in the database

The database is compiled and updated regularly by the manufacturer who has a large team of people looking at Web pages and classifying them appropriately. Because the database changes quickly, the URL filter system downloads a new copy automatically every night or every week.

As well as blocking obviously unsuitable material, these systems are useful for logging your organization's Web usage – for charging purposes or just to understand your network activity patterns better.

Some organizations control personal (non-work-related) surfing by blocking:

+   - advertisements
+   - instant messaging and chat
+   - streaming audio/video, MP3 sites
+   - shopping, share dealing
+   - "reality TV" sites