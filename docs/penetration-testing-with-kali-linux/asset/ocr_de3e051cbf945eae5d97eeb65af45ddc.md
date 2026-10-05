# OffSec

Penetration Testing with Kali Linux

Figure 121: Mountain Desserts Single Page Application

Figure 121 shows the page after we open it in a browser. The navigation bar displays a file named index.php, so we can conclude that the web application uses PHP. To gather more information about the page's structure, we should hover over all buttons and links, collecting information about parameters and the different pages we come across.

![](bbox=[0.122, 0.209, 0.878, 0.358])

Figure 122: Hovering over a Button

Scrolling down and hovering over all buttons and links, we'll notice most of them only link to the page itself, as shown in Figure 122.

At the bottom of page, we'll find a link labeled "Admin".

| mounttainindesserts.com/meteor/index.php?page=admin.php | Admin |

Figure 123: Hovering over the "Admin" link

Figure 123 shows the link preview when we hover over the Admin link with our cursor, displaying the URL http://mountaindesserts.com/meteor/index.php?page=admin.php.

We know the web application uses PHP and a parameter called "page", so let's assume this parameter is used to display different pages. PHP uses $_GET^286 to manage variables via a GET request. When we click on the link, we receive an error message stating the page is currently under maintenance.

| 926 | 7 | SOLD MOUNTAIN DESSERTS | RECURRING CUSTOMERS |

The admin page is currently under maintenance.

^286 (PHP Manual, 2022), https://www.php.net/manual/en/reserved.variables.php

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

252