
## UPnP – the solution

The best way to protect against all these vulnerabilities is by disabling UPnP in your router (step-by-step instructions will be provided in the User's safety guide for wireless networks section). However, if you really need UPnP (to enhance the experience of a device), then you must follow these:

- Check the model of your router on the internet and verify that the manufacturer has released a patch for the vulnerabilities related to UPnP. In fact, in 2020, researchers found a vulnerability called CallStranger that enabled an attacker to exfiltrate data from your systems; therefore, if you want to have UPnP enabled, you must keep checking for vulnerabilities and make sure you patch them. To find the list of current vulnerabilities, please visit https://cve.mitre.org.
- Filter all external traffic trying to use UPnP.
- Monitor network traffic to find abuses of UPnP.

You may have a lot of technical and administrative controls at the office to secure your wireless network, but what about users working from home? Do they have the same level of security on their wireless connection at home?

This should be a major concern for you because maybe most of your users are now working from home, therefore it is imperative to establish and distribute clear guidelines (administrative controls) to the users to ensure they have acceptable levels of security to avoid additional risks to business data and systems.

## User's safety guide for wireless networks

The person in charge of security for your organization, you must provide guidance to the users to reduce the risks of attack.

Taking into consideration that most users use Wi-Fi to connect to the internet, then it would be a great idea to create a manual of best practices when using wireless networks and distribute it to all employees.

> Tip
Also, remember that the key here is to ensure that all users are familiar with these guidelines, so some good ideas would be to create infographics by share by email or create some cool videos to call people's attention to this campaign. Also, you can designate some influential employees as security champions to help you disseminate these strategies among all employees.

Most of the security settings are configured on the Wi-Fi router, so let's start by showing the steps to log on to the administrative console of the Wi-Fi.

## Accessing your router

Here are the five simple steps required to access your router settings:

1. Go to Google and enter the name of your router (brand and model) and the phrase admin password. For example, Linksys E1200 admin password.
2. Then click on the relevant link from the manufacturer (in this case, linksys.com).
3. As shown in the following figure, the link sent to the manufacturer support page, which confirms that the default username and password for your router are admin/admin:

![](img/8c6a223c57e25ea0cc1593903a1b920f_273_0.png)

## Linksys E1200 N300 Wireless Router Frequently Asked Questions

2. What are the default IP Address, username, and password of the Linksys E1200?

The default IP Address is 192.168.1.1 and the username and password are both "admin".

> Figure 8.10 – admin username and password

4. To access the router, you just need to type the IP address of the router into your browser. In this case, the support page mentions the default IP address; however, that address may change. But don't worry, this is very simple to confirm with the following steps:

a. Press + R to launch the Run window, then type cmd and hit Enter to open Command Prompt.
b. On Command Prompt, type ipconfig and hit Enter.

c. Then look for the value called Default Gateway – that will be the IP of router. And as shown in the following figure, this is different from the preceding default provided by the manufacturer, as one is 192.168.0.1:

```
C:\Users>ipconfig

Windows IP Configuration
Wireless LAN adapter Wi-Fi:

IPv4 Address . . . . . . . . . . . : 192.168.0.4
Subnet Mask . . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . . . : 192.168.0.1
```

Figure 8.11 – Router’s IP address

5. Once you type the IP address on your browser, it should prompt you with a login page asking for your credentials. In this example, both the username and password are admin.

> Tip
All interfaces are different (depending on the manufacturer), but the information should will be the same, so take some time to explore the interface and get familiar with it. Linksys has an emulator that you can use to get familiar with the interface at http://ui.linksys.com/E1200/1.0.

Let’s see what attributes you want to make here for your wireless router more secure.

## Admin password

As you just, the password of your router may be very weak (and known to everyone), so the very first step is to secure the router by changing it. Depending on the router, it could be under tab called Management, Security, Login, or Users.

> Tip – Use a passphrase
The longer password, the harder it is for an attacker to crack it, so use a phrase that you can easily remember as your password, for example, I.Love my.wife.since.2014, or something motivational like I.am.sure.I.will.get.masters.in.2021. Of course, these are just examples, but create one that is unique to you with at least 25 characters. As any other password, using special characters, slang, and popular phrases is better, because then your password will be strong against brute-force and dictionary attacks.

## Admin user

Attackers knows that the default username to connect to the router is normally admin, however some routers allow you to change that username. So, if you have option, it is highly recommended that you change that username as it will prevent most attacks as it will be targeted at a nonexistent user.

## Wireless password

As mentioned in the preceding section, the use of a strong (long) passphrase is recommended for your wireless network. Also, a good practice is to change it at least every 6 months.

## Wireless security (security mode)

Here you have three encryption options: WEP (highly insecure), WPA (vulnerable), WPA2 (recommended).

## Wireless network name (SSID)

By default, the SSID could be the brand of your wireless router plus some random numbers. This is not only ugly, but also dangerous because everyone will know the model of your router, attacking it will be easier. So, as a first step, change the name of your SSID to a name of your preference. Also avoid using your own name in the SSID that could make you an easier target. Therefore, an SSID like Harper Family should be avoided.

> Tip–2.4 GHz and 5 GHz
Most modern routers have two bands (2.4 GHz and 5 GHz) and in most cases, you need to configure them as if they are two different routers different SSIDs, different security modes, different passphrases, different guest accounts, and so on). Therefore, make sure that all settings are the same on both networks to avoid leaving holes in one of them.

## Guest accounts

Imagine your neighbor needs to connect to your Wi-Fi for a minute to send an urgent email. That means you need to reveal your ultra-secure passphrase, but now your passphrase is saved on their device, they can connect at any time they want. Now, if you change your passphrase to avoid that, then it means that you will have to re-enter the passphrase on all your devices. Therefore, to avoid all that, you can enable guest accounts. Guest accounts enable you to create an account for external people, which has a lot of advantages including the following:

- They can be enabled temporarily and disabled to prevent any further access.
- You can change the password any time you want without affecting your other devices.
- Since you can use them as temporary accounts, you can create a new password every time you use them, making it almost impossible to crack.

## Remote access

Some routers have the option for you to access the management console from a remote location (through the internet). This is very insecure as it opens the doors to attackers to gain access to your router (and then your network and data). Therefore, always disable the remote access feature.

## Disable WPS (both the button and PIN versions)

As mentioned in the preceding section, WPS is a highly vulnerable protocol that must be disabled (and is normally enabled by default).

To do so is very simple – just look for WPS settings on your router (as shown in the following figure) and click to disable WPS:

| 2.4G/5G WPS Settings |
| :--- | :--- |
| WPS Enable | |

Figure 8.12 – WPS settings
