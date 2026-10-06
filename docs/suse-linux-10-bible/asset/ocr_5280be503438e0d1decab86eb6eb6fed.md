# 482 Part IV ♦ Implementing Network Services in SUSE Linux

![](bbox=[0.181, 0.137, 0.818, 0.502])

Figure 17-3: Specifying your network connection

On this screen, you identify the type of network connection that is used by the host on which you are running sendmail. If you want to automatically include virus scanning as receiving incoming mail, click the Enable virus scanning (AMViS) check box. If this package is not already installed, YaST will prompt you for the appropriate CD or DVD media at the end of the sendmail configuration process.) After selecting the appropriate options on this screen, click Next. The next screen shown in Figure 17-4 displays.

If you are configuring sendmail on a host where you want to be able to receive and deliver mail, but your site uses a central server for relaying mail for the Internet or other local networks, enter the name of this central server on this screen. If sendmail will need to authenticate to this server in order to send mail through it, click Authentication and enter the name and password of the user sendmail should use (This is often a user named "sendmail," for whom a specific account has been created.) Click OK to record any changes that you have made and return to the Outgoing mail pane, or click Back to return to the Outgoing mail pane without making any changes.