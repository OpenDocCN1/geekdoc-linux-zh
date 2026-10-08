As a hacker/pentester, this can be invaluable information! It means that this system was last rebooted nine days ago. If a recent patch has been released for a known vulnerability within those nine days, we can conclude that this system has NOT been patched and is probably vulnerable to that known exploit.

# **Website Active Reconnaissance Nmap and hping3 are wonderful tools for actively determining critical elements of any system such as ports, services and operating system. When scanning websites, we need to use a different set of tools.**

Websites are built using a variety of technologies (see [Web Technologies](#) here ). In most cases, before we develop a hacking strategy of the website, we need to understand the technologies employed in building it. Website attacks are not generic. For instance, attacks against WordPress-based websites won't work against .NET based websites and vice versa. We need to do this type of reconnaissance first before progressing to compromising a website.

WhatWeb is a Python script that probes the website for signatures of the server, the CMS and other technologies used to develop the site. According to the WhatWebweb page: WhatWeb recognises web technologies including content management systems (CMS), blogging platforms, statistic/analytics packages, JavaScript libraries, web servers, and embedded devices. WhatWeb has over 1700

> *plugins, each to recognise something different. WhatWeb also identifies version numbers, email addresses, account IDs, web framework modules, SQL errors, and more.*

Once we know what technologies the website is running, we can run vulnerability scans to find known vulnerabilities and