# Chapter 17 + Mail Servers – Postfix, Sendmail, Qpopper, and Cyrus 483

![](bbox=[0.179, 0.137, 0.821, 0.506])

If you want mail from the host that you are configuring to appear to be from a different domain, click Masquerade and enter the information about that you want to appear in the headers of mail sent by sendmail. This panel also enables you to configure sendmail to make mail from specific local users appear to come from selected locations, which can be useful for system accounts that do not want to reflect the name of the specific host from which they were sent. Click OK to record any changes that you have made and returned to the Outgoing mail pane, or click Back to return to the Outgoing mail pane without making changes.

Click Next to continue the configuration process and display the screen shown in Figure 17-5.

The most important setting on this panel is the Accept remote SMTP connections setting. By default, sendmail listens on a system's loopback interface and uses that to locally deliver mail that has also been sent locally. You will need to enable the Accept remote SMTP connections setting if you want your system to be able to accept and deliver mail sent from other systems (such as if you are setting up a system that will deliver or relay mail sent by other systems).