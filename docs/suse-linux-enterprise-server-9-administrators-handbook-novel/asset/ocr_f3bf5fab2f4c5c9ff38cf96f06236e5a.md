# NOTE

Visibility is an important factor to keep in mind when you are deploying web-based tools. When you deploy an ACID website, ask yourself who has access to it. By default, websites are available to anyone who finds them.

Is it acceptable for you to show the world which events tripped your Snort sensor? If an attacker can also monitor your monitoring of network activity, could he change his approach and become more stealthy?

There are a number of steps you might want to take to secure your website:

+   - You can set up a firewall rule to accept connections only from specific TCP/IP addresses.
+   - You can also set up a robots.txt file. This keeps spiders from adding your website to Google and other search engines. It does not, however, prevent spiders that do not obey robots.txt files.
+   - You can enable SSL on the site and configure your web browser to support .htaccess files. This encrypts your HTTP conversations and adds a simple level of challenge-response protection to your site's content.

Keep in mind that the tools you deploy, unless secured, can be used against you.

**FIGURE 12.6**
The ACID main menu.

![](bbox=[0.181, 0.577, 0.767, 0.855])

On this page, you immediately get a significant amount of information not immediately apparent from the flat log files. You can quickly see the alert