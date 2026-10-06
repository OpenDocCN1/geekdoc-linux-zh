
# 480 Part IV ♦ Implementing Network Services in SUSE Linux

freely available. Development of sendmail continues in both the Open Source community (www.sendmail.org) and at a company named Sendmail (www.sendmail.com), where Eric Allman is CTO, and a next-generation version of sendmail is actively under development.

This section explains how to install, configure, and initiate sendmail on a SUSE system.

## Installing sendmail

As mentioned previously, sendmail is never installed by default on a SUSE system. To install sendmail, you will need to remove Postfix, the default MTA on SUSE Linux systems, or any other MTA that you may have previously installed. SUSE's use of RPM as a core database for tracking installed packages and associated files simplifies adding and removing entire packages, YaST makes the process even easier.

To install sendmail on your SUSE system:

- 1. Install YaST, select Software, and finally, select Install and Remove Software. Click the Administrator Mode and enter the system's root password to proceed to the actual installation screen.
- 2. To locate the sendmail package, enter sendmail in the Search box and click the Search. The sendmail package displays the package list at the top right of this dialog. Click the check box to indicate that you want to install the package and the Accept button in the lower right portion of the Install and Remove Software.
- 3. If you configured your SUSE system as a server system, YaST automatically installed Postfix for you as part of the basic server installation. If this is the case, YaST displays the Dependency Conflict box shown in Figure 17-2. As you can see from this figure, YaST automatically detects sendmail conflicts with the Postfix MTA that is currently installed.
- 4. If the media containing the sendmail package is not already in your CD or DVD drive, YaST prompts you to insert the appropriate CD or DVD and proceeds with the installation.
- 5. After installation is complete, YaST displays a dialog asking if you want to install other packages. Click No and then click OK to close YaST's Install and Remove Software pane.

To resolve this, click the Remove the Conflicting button, which is shown in Figure 17-2. Click OK - Try Again to proceed.

# Chapter 17 + Mail Services — Postfix, Sendmail, Qpopper, and Cyrus 481

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_525_0.png)

Figure 17-2: YaST's dependency conflict dialog

## Configuring sendmail

sendmail's primary configuration information is stored in the file /etc/sendmail.cf. Additional information is stored in the directory /etc/mail. The file /etc/sendmail.cf is a text file that contains configuration information consists of name/value pairs on separate lines of the file.

Most systems that run sendmail create the file /etc/sendmail.cf from another file, sendmail.mc, which is often stored in the /etc/mail (Linux systems such as Red Hat) or /usr/lib/mail/cf (Solaris) directory. The file sendmail.cf is generated from sendmail.mc using the m command, which is a macro processor that expands the condensed information in sendmail.mc into a more complete sendmail.cf.

Luckily, SUSE simplifies sendmail configuration by providing a graphical configuration mechanism in YaST. The YaST configuration module for sendmail and the shell scripts and configuration files it uses are all automatically installed as part of SUSE package. Configuring any MTA in YaST is done in the same location, which is Network Services Mail Transfer Agent. The underlying scripts implement any changes or additional options provided by different support MTAs on SUSE Linux, such as Postfix, sendmail, and Exim. This section describes the most common configuration options that you may want to set or change in YaST's sendmail configuration module.

After starting YaST's MTA configuration module (Network Services -> Mail Transfer Agent), the screen shown in Figure 17-3 will appear.

# 482 Part IV ♦ Implementing Network Services in SUSE Linux

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_526_0.png)

Figure 17-3: Specifying your network connection

On this screen, you identify the type of network connection that is used by the host on which you are running sendmail. If you want to automatically include virus scanning as receiving incoming mail, click the Enable virus scanning (AMViS) check box. If this package is not already installed, YaST will prompt you for the appropriate CD or DVD media at the end of the sendmail configuration process.) After selecting the appropriate options on this screen, click Next. The next screen shown in Figure 17-4 displays.

If you are configuring sendmail on a host where you want to be able to receive and deliver mail, but your site uses a central server for relaying mail for the Internet or other local networks, enter the name of this central server on this screen. If sendmail will need to authenticate to this server in order to send mail through it, click Authentication and enter the name and password of the user sendmail should use (This is often a user named "sendmail," for whom a specific account has been created.) Click OK to record any changes that you have made and return to the Outgoing mail pane, or click Back to return to the Outgoing mail pane without making any changes.

# Chapter 17 + Mail Servers – Postfix, Sendmail, Qpopper, and Cyrus 483

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_527_0.png)

If you want mail from the host that you are configuring to appear to be from a different domain, click Masquerade and enter the information about that you want to appear in the headers of mail sent by sendmail. This panel also enables you to configure sendmail to make mail from specific local users appear to come from selected locations, which can be useful for system accounts that do not want to reflect the name of the specific host from which they were sent. Click OK to record any changes that you have made and returned to the Outgoing mail pane, or click Back to return to the Outgoing mail pane without making changes.

Click Next to continue the configuration process and display the screen shown in Figure 17-5.

The most important setting on this panel is the Accept remote SMTP connections setting. By default, sendmail listens on a system's loopback interface and uses that to locally deliver mail that has also been sent locally. You will need to enable the Accept remote SMTP connections setting if you want your system to be able to accept and deliver mail sent from other systems.

# 484 Part IV ♦ Implementing Network Services in SUSE Linux

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_528_0.png)

Figure 17-5: Specifying incoming mail parameters

The other settings on this panel enable you to specify a port for sendmail can retrieve and send mail, and to include a remote mail server from sendmail should retrieve mail for local delivery.

This panel also enables you to specify a central address to which you would like to be delivered. This is the most common example of mail aliasing, which is the ability to specify the destination to which mail addressed to a local user should be forwarded or delivered. Clicking the Alias button displays a screen that enables you to add other email aliases, which will be stored in the file /etc/mail/aliases. Similarly, clicking the Virtual domains button enables you to specify the destination to which mail addressed to non-local users should be forwarded or delivered.

Click Finish to complete your configuration of sendmail. If you have enabled antivirus scanning and the AmAV package is not already installed, YaST will prompt you for the appropriate CD or DVD media at this point. If this is the case, insert the appropriate media and wait for the installation to complete.

YaST completes the sendmail configuration process by running SUSEConfig for, which generates and updates /etc/sendmail.cfg for you, as well as any of the files in /etc/mail that have been affected by your configuration changes.
