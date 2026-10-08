![](bbox=[0.11, 0.12, 0.25, 0.23])

Red Hat permits you to register, for free, one computer for basic update service. Basic service allows you to download and install updated RPM packages. To update more machines, you have to purchase additional subscriptions at $60 per year. Note that you can register more machines under the Red Hat Network service, but they aren't eligible for updates.

# ## Reducing your exposure: Removing and reducing services

Hackers look for computer vulnerabilities by probing for vulnerable network services. Network services — such as Apache, Samba, and DHCP — are, of course, designed to respond to network queries. Therefore, hackers can readily find out what services you run and then find which, if any, attacks to use.

We describe elsewhere how keeping software updated minimizes your vulnerability. However, you can go one step better and make a service invulnerable by turning it off. One simple security rule is “Keep it simple.” The simple fact is that if you don't need to run a service, you shouldn't.

We describe in this section how to eliminate or reduce both network and non-network services. This section describes how to use the `chkconfig` utility to change the startup scripts that control when, how, and whether a network services starts at boot time:

+   1.  Click the **GNOME Menu** and choose **System Settings**:Server Settings:Services. Enter the root password if you're prompted.
    The Service Configuration window opens.
2.  Select an unnecessary service and shut it off by clicking the **Stop** button.
3.  Click the **OK** button when the confirmation window appears.
4.  Click the check mark to the left of the service to remove the check mark.
    Removing the check mark prevents the service from starting automatically at boot time.
5.  Repeat Steps 2–4 for each unnecessary service.
6.  When you have turned off each unnecessary service, click the **Save** button.
7.  Choose **Quit** from the **File** menu.

Which services you turn off depends on your needs, of course. For example, if you're unintentionally running a web server, turn off the `httpd` service. You generally should be able to turn off these services: