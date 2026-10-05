# OffSec

Penetration Testing with Kali Linux

We should also search for potential vulnerabilities in Apache 2.4.52 as we did for hMailServer. As this will yield no actionable results, we'll skip it.

We will begin by browsing the web page. Because the Nmap scan provided the HTTP title BEYOND Finances, with comments of encountering a non-default page are high.

![](bbox=[0.125, 0.243, 0.875, 0.538])

# BEYOND Finances

We are BEYOND Finances. A world leader in providing financial assistance to small and medium sized businesses.

![](bbox=[0.378, 0.543, 0.622, 0.553])

Figure 290 shows us a basic web page. However, if we review the web site, we'll notice it doesn't contain a menu bar or links to other pages. At first glance, there seems to be nothing actionable for us.

Let's inspect the web page's source code to determine the technology being used by right-clicking in our browser on Kali and selecting View Page Source. For a majority of frameworks and web builds, such as CMS's¹¹¹/⁹ we can find attributes and strings in the source code.

Let's browse through the source code to confirm the example to the page header, comments, and links. At the bottom, we find some links as shown in the following figure:

```
198 <script src="https://192.168.50.240/wp-content/plugins/contact-form-7/includes/form-control.js?ver=5" id="contact-form-7-js"></script>
197 <script src="https://192.168.50.240/wp-content/themes/elementor/assets/js/frontend.min.js?ver=3" id="elementor-frontend-js"></script>
196 <script src="https://192.168.50.240/wp-content/themes/elementor/assets/js/frontend.min.js?ver=3" id="elementor-pro-frontend-js"></script>
195 <script src="https://192.168.50.240/wp-content/themes/elementor/assets/js/pro-frontend.min.js?ver=3" id="elementor-pro-frontend-js"></script>
194 <script src="https://192.168.50.240/wp-content/themes/elementor/assets/js/widgets.min.js?ver=3" id="elementor-widgets-js"></script>
193 <script src="https://192.168.50.240/wp-content/themes/elementor/assets/js/common.min.js?ver=3" id="elementor-common-js"></script>
192 <script src="https://192.168.50.240/wp-content/themes/elementor/assets/js/frontend.min.js?ver=3" id="elementor-frontend-js-"></script>
```

Figure 291: Landing Page of WEBRSV1

We notice that the links contain the strings "wp-content" and "wp-includes". By entering these keywords in a search engine, we establish that the page uses WordPress.

¹¹/⁹ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Content_management_system

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

812