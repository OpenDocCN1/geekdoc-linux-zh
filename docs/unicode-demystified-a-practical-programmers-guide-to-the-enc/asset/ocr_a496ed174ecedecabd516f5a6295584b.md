# Chapter 17 Red Hat Linux System Administration

![](bbox=[0.395, 0.04, 0.705, 0.315])

Figure 17-11 Local Samba/swat home page

+   * Click swat to put a check mark in the check box.
* Make sure that a check mark is in the box next to xinetd; click to highlight the xinetd line.
* Click Restart on the toolbar.
* Click Save on the toolbar.
* Click Exit on the toolbar.

Now you should be able to open a browser, enter http://127.0.0.1:901 or http://localhost:9001 in the location bar, and give the username root and the root password in response to swat's request to display the local Samba/swat home page (Figure 17-11). This page has local links to Samba documentation and buttons that display other windows. You can access this page from other systems, but doing so means that your password is sent in cleartext over whatever connection you are using.

It is easy to establish a basic Samba setup so that you can see a partition for your GNU/Linux drive on an MS Windows machine (any version of Windows from 3.1 on). More work is required to set up a secure connection or with special features. The following example uses swat to create a basic setup. Each of the options that you configure has the word Help next to it. Click Help, and a new browser window containing an explanation of the option appears. For this example