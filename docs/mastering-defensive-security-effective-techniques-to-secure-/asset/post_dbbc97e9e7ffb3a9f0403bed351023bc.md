
Now that you know these great Wi-Fi tools (hardware and software), it is time to move on and look at another exciting topic: pentesting.

## Pentesting tools and methods

There is a common misconception that pentesting = networking testing, and that is a huge mistake.

As a master in defensive security, you need to drive your defensive strategy in an integral way by including all the actors, factors, and actions that may impact your infrastructure.

Therefore, in this section, we will be exploring all the different tools and methods that you need to leverage to create the most comprehensive and powerful cybersecurity strategy.

## Metasploit framework

Metasploit is considered an exploitation framework, which means it's a powerful pack of tools and utilities that you can leverage to test your infrastructure.

It includes a variety of tools that can be used for the following purposes:

- Information gathering (passive and active)
- Vulnerability scanning
- Exploitation
- Post-exploitation
- And many other additional modules including some to help the attacker to cover its tracks

The intent of this book is not to focus on the offensive part, but it will be valuable for you to know the basics about this tool. Due to this, we will be covering this in depth in Chapter 15, Leveraging Pentesting for Defensive Security.

## Social engineering toolkit

This is a very powerful toolkit used most by attackers; however, you can also take advantage of this tool to develop the following:

- Awareness campaigns.
- Improved training.
- Realistic labs.
- Assess the susceptibility of the users to a given attack.

> Tip
> As we mentioned previously, showing the susceptibility of the employees to a given attack (for example, demonstrating that 60% of the employees put their credentials on a fake page) is a great way to get support and a budget from upper management.

As shown in the following screenshot, the **Social Engineering Toolkit (SET)** is an all-in-one toolkit that contains all the utilities that you need to create realistic and engaging awareness campaigns:

```
File Actions Edit View Help
---------------------------
[ ] The Social-Engineer Toolkit (SET) [ ]
[ ] Created by: David Kennedy (ReLIK) [ ]
Version: 8.0.3
Codename: Maverick *
Follow up on Twitter: @trustedSec [ ]
Follow me on Twitter: @hackingDave [ ]
Homepage: https://www.trustedsec.com [ ]
Welcome to the Social Engineering Toolkit (SET).
The one stop for all of your SE needs.

The Social-Engineer Toolkit is a product of TrustedSec.
Visit: https://www.trustedsec.com

It's easy to update the PentTesters Framework! (PTF)
Visit https://github.com/trustedsec/ptf to update all your tools!

Select from the menu:
1) Spear-Phishing Attack Vectors
2) Website Attack Vectors
3) Infectious Media Generator
4) Create a Payload and Listener
5) Mass Mailer Attack
6) Androidline-Based Attack Vector
7) Wireless Access Point Attack Vector
8) QRCode Generator Attack Vector
9) PowerShell Attack Vectors
10) Third Party Modules

99) Return back to the main menu.
```

Figure 5.4 – The main menu of the Social Engineering Toolkit (SET)

Now, let's take a look at the most important aspects of these tools:

- **Spearphishing attack vectors**: This is a great tool that you can leverage to test whether your employees are susceptible to **phishing attacks**. Here, you can craft the message so that it's as realistic as possible. Additionally, the tool lets you include a payload if needed.

If you want to take this test to the next level, you can even spoof email addresses to challenge more technical teams.

As shown in the following screenshot, the tool gives you the option to create an automated attack. You can even customize based on a variety of options:

```
The **Spearphishing** module allows you to specially craft email messages and send them to a large (or small) number of people with attached file malicious payloads. If you want to spoof your email address, be sure "Sendmail" is installed (apt-get sendmail) and change the config/set_config SENDMAIL-OFF flag to SENDMAIL-ON.
```

There are two options, one is getting your feet wet and letting SET do for everything for you (option 1), the second is to create your own FileFormat payload and use it in your own attack. Either way, good luck and enjoy!

1) Perform a Mass Email Attack
2) Create a FileFormat Payload
3) Create a Social-Engineering Template

> Figure 5.5 – SET Spearphishing module

- **Web attacks**: Here, you have a variety of options to play with. The most common is website cloning, in which the user clones a frequently visited website (like a social media site). Then, when the user accesses the site, it will be sent to a fake site where you have full control to inject malicious code and harvest user credentials.

Harvesting credentials is a very dangerous task - in fact, the recommendation is not to save the user credentials. Instead, once the user inputs the credentials, the button will just display a message, stating that this was a cybersecurity test and their credentials could be compromised by others using this method by not capturing those.

> Tip
> Never harvest credentials without proper written authorization from the legal department. This is because you need proof that the company are aware of the activity that you are performing (especially if you are a third party hired to perform this test), but also because legal teams need to be involved to ensure alignment with regulations and laws.

## Cybersecurity Technologies and Tools

Additionally, instead of injecting malicious code, you can create some HTML that tells the user this was a security test, but next time it could be a real attack. This technique will help increase awareness between users.

As shown in the following screenshot, you can leverage additional attack mechanisms, such as HTAs, web jacking, and more:

| Method | Description |
| :--- | :--- |
| Web Attack | A unique way of utilizing multiple web attacks in order to compromise the intended victim. |
| Java Applet | Will spoil a Java Certificate and deliver a payload. Uses custom java applet created by Thomas Werth. |
| Metasploit Browser | Will select metasploit exploits through an iframe and deliver a payload. |
| Credential Harvest | Utilize cloning of a website that has username and password field and harvest all the information posted to the website. |
| Tabnabbing | Will wait for user to move to a different tab, then refresh the page to something different. |
| Web Jack | Introduced by white_sheep; utilizes replacements to make the highlighted URL link appear legitimate however when clicked a window pops up then replaced with the malicious link. Can edit link replacement settings in set_config if its too slow/fast. |
| Multi-Attack | Will use a combination of attacks through the web attack. For example you can utilize the Java applet, metasploit Browser, Credential Harvest/Tabnabbing all at once to see which is success. |
| HTA Attack | Allows you to clone a site and perform powershell injection through HTA files which can be used for Windows-based powershell. |

1) Java Applet Attack Method
2) Metasploit Browser Exploit Method
3) Credential Harvest Method
4) Tabnabbing Method
5) Web Jacking Attack Method
6) Multi-Attack Web Method
7) HTA Attack Method

99) Return to Main Menu

Figure 5.6 – SET web attack module

**Infectious media generator:** With this tool, you can create an inf file that will be automatically executed when the device (USB, DVD, CD) is inserted.

Here, you can get a cheap USB and load it with this utility to determine how vulnerable employees are falling into this trap.

Since this attack requires investing in the necessary hardware, it is recommended to do this on a targeted population, such as company executives, to determine their likelihood to insert an unknown USB device.
