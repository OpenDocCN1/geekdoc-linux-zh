# Linux Web Server Toolkit

# WHAT TYPE OF BROWSER IS MOST USED BY VISITORS TO MY SITE?

Not all statistics programs report the percentage of browser use, and not all browsers report themselves either. If a statistic for browser type is available via your statistics package, it will give a percentage for each of the browsers reporting their names and versions, so you'll know how many people are using Netscape Navigator on which platforms (Macintosh, Windows 95, etc.) and how many people are using Lynx, Microsoft Explorer, and all the other browser variants.

Having these features is very helpful in telling you how to provide the best service for visitors to your site. If 90 percent of your visitors are using Netscape Navigator Gold on Linux, for example, you can use advanced features like JavaScript in all your pages, and you can turn on gzip compression capability to save downloading time. If most of your visitors are on Windows systems (a likely scenario, actually), you may not want to bother with gzip compression because most cannot use it. Instead, you can find a Linux version of the pkzip utility that's on DOS machines.

On the other hand, if many of your visitors are using the Lynx browser, popular character-mode Web browser, you'll want to be certain you're not relying on graphics for key information on your pages because all visitors who Lynx won't be able to see.

In general, you'll want to test your pages on any browser that is used by more than 5 percent to 10 percent of your visitors. Test a larger variety—down to 1 percent—if you have a larger site and more resources. If you don't have the resources to do this type of testing, at least view your pages on Microsoft Internet Explorer and the latest versions of Netscape Navigator and Netscape Communicator.

![](bbox=[0.175, 0.625, 0.255, 0.695])

To create statistics for User Agents (browsers), you must include the AgentLog directive in the srm.conf file and compile the mod_log_agent module into the Apache Web server.

# ARE MANY OF MY VISITORS FROM EDUCATIONAL INSTITUTIONS OR GOVERNMENT AGENCIES?

Just answering the question about international visitors, knowing from the domain name lists whether a large percentage of your visitors are from educational institutions (with an .edu domain) or from government agencies (with a .gov domain) can guide you in determining who is most interested in your site, how people are finding your site, and how you can reach the people you want to reach and appeal to those who are visiting your site.