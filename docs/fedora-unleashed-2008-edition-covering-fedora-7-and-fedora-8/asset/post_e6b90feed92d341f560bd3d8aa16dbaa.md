
## Mozilla Firefox

One of the most popular web browsers, and in fact the default web browser in Fedora, is Mozilla Firefox (see Figure 5.1). Built on a solid code base that is derived from the original Mozilla Suite, which itself comes from Netscape, Firefox offers a breath of fresh air to surfing the Internet, compared to the dominant Internet Explorer (which is only available on Windows). Firefox offers a secure browsing environment, coupled by the ability to extend the browsing experience by using plug-ins and extensions, which we cover briefly later in this section. There have been more than 416 million downloads of Firefox since its release in the middle of 2005, and it has grabbed significant market share from Internet Explorer.

In Fedora, you can find Firefox under the *Applications, Internet* menu at the top of your screen. An even simpler way to start Firefox is to click the small *World* icon next to the *Actions* menu. Either way, Firefox opens.

![](img/34e72348d53ca54c2a1d9c871316691b_135_0.png)

**FIGURE 5.1** Mozilla Firefox—rediscover the Web. Firefox enables you to add on numerous upgrades, further enhancing your experience.

Beyond the basic program is a wealth of plug-ins and extensions that can increase the capabilities of Firefox beyond simple web browsing. Plug-ins such as Shockwave Flash and Java are available instantly, and are multimedia codecs for viewing video content, whereas extensions provide useful and sometimes humorous additions to the browsing experience. For example, ForecastFox is an extension that gives you your local weather conditions, and Bandwidth Tester is a tool that calculates your current bandwidth. Perhaps the best way to while away a lazy afternoon is to download the StumbleUpon extension, which provides you with the proverbial big red button that you can click to be taken to a web page based on certain predefined conditions that you select. More often than not you'll come across some Calvin and Hobbes strip that will make you smile just when you need it. However, you can find some real gems by using StumbleUpon. As Firefox grows, there will be more and more extensions and plug-ins that you can use to enhance your browsing pleasure.

Finding and obtaining these plug-ins and extensions is made very easy because Mozilla developers have helpfully created a site dedicated to helping you get more from Firefox. Particular favorites are the Adblock Plus and the StumbleUpon plug-ins. Adblock Plus allows you to nuke all those annoying banners and animations that take up so much bandwidth while you are browsing.

Another plug-in that we make a lot of use of is Google BrowserSync. If, like us, you work across multiple computers, you will no doubt have had to re-create bookmarks at every different computer and try to keep them the same. Google makes this whole process much easier by allowing you to synchronize not only your bookmarks, but also your cookies, browser history, and finally any saved passwords across multiple browsers. Bear in mind that you can choose what you want to synchronize, making it easy just to replicate your bookmarks.

## Konqueror

KDE users have the option to use Konqueror, which is the default browser for KDE (see Figure 5.2). As well as handling file system navigation, Konqueror can be used to surf the Web. It, too, is based on the Gecko rendering engine as found in Firefox.

![](img/34e72348d53ca54c2a1d9c871316691b_136_0.png)

**FIGURE 5.2** Konqueror, the standard KDE web and file system browser.

## Choosing an Email Client

Back in the days of UNIX, there were various text-based email clients such as `elm` and `pine` (Pine Is Not Elm). Although they looked basic, they allowed the average user to interact with his email, both for composing and reading correspondence. With the advent of mainstream computing and the realization that people needed friendly GUI interfaces to be productive came a plethora of email clients, with some of them being cross-platform and compatible among Linux, Windows, and Mac OS X, not to mention UNIX.

### Evolution

Evolution is the standard email client that comes with Fedora, and to call it an email client would be to sincerely underestimate its usefulness as an application. Not only does it handle email, it can also look after contacts and calendaring and can manage your tasks (see Figure 5.3). The next section demonstrates how to configure Evolution to handle email.

![](img/34e72348d53ca54c2a1d9c871316691b_137_0.png)

**FIGURE 5.3** With Evolution, you can handle all your email and contacts and make appointments and track tasks.

You need to have the following information to successfully configure Evolution:

- Your email address
- Your incoming email server name and type (that is, pop.email.com, POP, and IMAP)
- Your username and password for the incoming server
- Your outgoing email server name (that is, smtp.email.com)

After you have all the information, you can start Evolution. The first screen you are presented with is the Identity screen as part of the Account Setup Assistance Wizard (see Figure 5.4).

![](img/34e72348d53ca54c2a1d9c871316691b_138_0.png)

**FIGURE 5.4** You can launch and configure Evolution with just a few simple commands. The Identity screen, the first of several screens, asks you to enter your information. Click Forward to proceed.

The next screen permits you to configure Evolution to use your mail transfer agent (MTA; the software used to transfer your mail from your computer to the wider network or Internet). You can choose POP, IMAP, the local spools found in /var/mail in either mbox or maildir format, a local MTA, or None if you simply want to use the other features of Evolution. As shown in Figure 5.5, you can also set your password.

Now you can select options that govern how Evolution handles incoming email. Here you can choose the frequency at which Evolution checks for email (check the box to get Evolution to check for emails every 10 minutes), as well as what Evolution should do with message storage; but, to be honest, we'd keep these specific settings unchecked. Click the Forward box to proceed.

> **TIP**
> If you connect to the Internet using a dialup modem, make sure you don’t check the Checking for New Mail option; otherwise, you might find that you will be connecting every 10 minutes.

![](img/34e72348d53ca54c2a1d9c871316691b_139_0.png)

**FIGURE 5.5** The Receiving Mail screen requires information from your ISP or system administrator.

You must also choose between SMTP or Sendmail for sending your mail; enter your email address, and choose a time zone (very important for your calendar). Finally, you will see the opening Evolution window in Figure 5.6.

![](img/34e72348d53ca54c2a1d9c871316691b_140_0.png)

**FIGURE 5.6** The standard Evolution display. On the left, you can see buttons to choose Mail, Contacts, Calendars, and Tasks windows.

Each icon in the left pane of the main Evolution window opens a different window when selected. Each view has options that can be configured to suit your needs; you’ll find access to the preferences dialog box under the Edit menu, which is shown in Figure 5.7.

![](img/34e72348d53ca54c2a1d9c871316691b_140_1.png)

**FIGURE 5.7** The calendar application Tools screen is where the information can be shared with others. Here you can configure the times and dates.

### Mozilla Thunderbird

Mozilla Thunderbird (see Figure 5.8) is the sister program to Firefox. Whereas Firefox is designed to browse the web, Thunderbird's specialty is communication. It can handle email, network news (see later in this chapter), and RSS feeds.

![](img/34e72348d53ca54c2a1d9c871316691b_141_0.png)

**FIGURE 5.8** The natural companion to Firefox, Mozilla's lightweight email client Thunderbird can be found in use all over the world.

Thunderbird is not installed by default with Fedora, so you will have to use either Add/Remove Packages or yum to install it. As with Firefox, there are many plug-ins and extensions to enhance your email and news reading.

### KMail

If you are using the KDE Desktop Environment rather than the Fedora default GNOME desktop, you will also have KMail installed. As with Balsa, it will not take users of Outlook Express or Mozilla Mail very long to get used to the KMail interface. Some useful features found in KMail are the choice of mbox or maildir formats, improved filter creation, the capability to sort mail into threads, and the capability to apply filters at the MTA. Figure 5.9 shows the KMail email program. KMail offers IMAP access, extensive filtering, mbox and maildir formats, and the capability to easily integrate MTAs such as Procmail, Spamassassin, or custom processing scripts.
