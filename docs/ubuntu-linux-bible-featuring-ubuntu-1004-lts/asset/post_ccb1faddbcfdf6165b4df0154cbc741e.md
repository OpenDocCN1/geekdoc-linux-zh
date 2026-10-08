
# Part II: Ubuntu for Desktop Users

friends is probably more important than philosophy. The good news is that because most instant messaging accounts are free, you can sign up with as many instant messaging services as you want and then use a multi-protocol client to communicate with all of your friends at any of them.

# Note

If you're already using a free Mail service like AOL, Microsoft Live/Hotmail, Google, or Yahoo, you probably already have an instant messaging account through the same service. Log in and look for an FAQ (Frequently Asked Questions file) or general information about IM support. In most cases, your IM identify is the same as your e-mail address, without any domain information. If your e-mail address is wonhagen@yahoo.com, your IM identity is almost certainly wonhagen.

The following is a list of some popular locations where you can sign up for free instant messaging accounts:

- AIM: AOL's acquisition of Mirabilis's ICQ software made AIM (Instant Messenger) the original leader in the instant messaging space, and it is still one of the most popular IM sites around. You can get a free ID (known as a screen name because of its roots in AIM) www.aim.com, which comes with an equivalent aim.com e-mail account. Similarly, you can get an AIM account by registering for free e-mail with AOL (www.aol.com). The underlying communications protocol used by AIM is called Oscar.
- Jabber: Be far it from Google to miss out on any aspect of life. Google (www.google.com/talk) is Google's instant messaging platform, which you can access through the same Google account that you use for Gmail. If you do not have a Google account, launching Google Talk provides links through which you can create one. Not surprisingly, Google Talk uses a browser interface for instant messaging and chats, so it works almost anywhere. Google Talk uses XMPP (Extensible Messaging and Presence) as its protocol.
- ICQ: Although still focused on numeric IDs, ICQ popularized instant messaging and is still a popular site. You can register for an ICQ account at https://www.icq.com/register. AOL bought ICQ long ago, ICQ also uses Oscar as its underlying protocol.
- Jabber: Jabber is an instant messaging platform where, as its PR material states, "your messages are not monitored by a big company like AOL, Microsoft, or Yahoo." (Instead, it's monitored by a very tiny company) Jabber uses the XMPP (Extensible Messaging and Presence Protocol), which is also used by Google Talk. To register for Jabber, your IM client will automatically create an account for you when you use any of the sites that Jabber uses (www.jabber.org/im-services for free).
- Microsoft: Microsoft provides free Live-accounts (formerly Hotmail), which come with a free Windows Live Messenger (formerly known as MSN Messenger) because all of your Microsoft accounts share the same identity. See http://login.live.com to sign up for an account. I know you'll be surprised to learn that Microsoft uses its own, proprietary IM protocol for instant messaging.
- Yahoo: Yahoo has provided an instant messaging service for a while, and its Yahoo Messenger is quite popular. You get instant messaging capabilities when you sign up for a Yahoo e-mail account (www.yahoo.com). Like Microsoft, Yahoo uses its own protocol for instant messaging.

# Chapter 10: Sending and Receiving Instant Messages

These are just the big names in the IM space. See the subsequent sections of this chapter on Pidgin and Empathy for information about the protocols that are supported by each of these instant messaging clients.

Although I'll admit to being a little afraid of Googlezilla, if I WERE to suggest one of the sites for your own IM pleasure, I'd vote for Google Talk, simply because you can use Gmail and the many other useful Google tools. It is open source software that uses a standard protocol, Jabber is a close second, especially if most of your IM friends are also Linux fans. If not, Yahoo and AIM are your best bets.

# Instant Messaging on Ubuntu with Empathy

Empathy is the instant messaging client that is installed by default on the latest Ubuntu Desktop systems. Empathy replaces an older instant messaging client Pidgin, which is still popular and is discussed in the following section of this chapter. Open source software is all about choice, after all!

Empathy is a multi-protocol instant messaging client that enables you to send and receive instant messages from AIM, Facebook Chat, Google Talk, GroupWise, IRC, Jabber, MSN, MySpace, SIP, Yahoo!, and many other instant messaging services. Empathy uses an underlying framework known as Telepathy that interfaces with standard, lower-level communication mechanisms used to exchange messages. For end users like you and me, this means Empathy is not limited to just instant messaging, but can also handle video chat and Voice Over IP (VoIP). Telepathy can also be extended to handle new communication mechanisms and associated protocols as they emerge from universities, the open source community, and tomorrow's hot spots.

# Starting Empathy

Ubuntu provides two ways to interact with Empathy:

- By selecting the Applications Internet Empathy IM Client menu item to actually start Empathy
- By using the panel's Menu applet, shown in Figure 10-1. This applet enables you to configure your active instant messaging account(s) in Empathy, displays your current status, and watches for incoming conversations, displaying an OSD (On-Screen Display) notification when an instant message is received from any of your buddies on any instant messaging account.

This app only informs you about incoming messages—it doesn't start Empathy for you. The OSD notification displays both the message and the name of the buddy that initiated it. Once you start Empathy, any buddies from incoming list but unanswered messages have been received will be blinking in the "Contact List" dialog.

# Part II: Ubuntu for Desktop Users

FIGURE 10-1

Ubuntu's MeMenu applet

![](img/1a233c34336fbf5a85d6eb785e401709_401_0.png)

Before you can actually use Empathy, you must configure at least one instant messaging account of some sort, as explained in the next section.

# Tip

If you are currently using Pidgin on another system, you can import the accounts that are defined on that system into Empathy by creating an archive file of the directories that contain Pidgin account information, transferring that file to your new system, and extracting its contents before starting Empathy for the first time. To do this, execute the following command on a system upon which your Pidgin accounts have been defined:

```
cd ~ ; tar jcvf dot-pidgin-files.bz2 .gaim .purple
```

Transfer this file to the machine upon which you will be using Empathy, and extract its contents using a command like the following:

```
cd ~ ; tar jxf dot-pidgin-files.bz2
```

The first time that you start Empathy on the system where you extracted the contents of this archive file, Empathy will detect the Pidgin configuration information and offer to import it.

If you didn't read this tip before starting Empathy for the first time, you can trigger Empathy's initial setup dialog by terminating all processes with telemetry in their name, terminating the empathy process, and then recursively removing the ~/.mission-control directory (in your home directory), which is where Telepathy clients as Empathy store account information. You can then start Empathy, and it will go through the initial setup account that is discussed in the next section.

# Configuring Instant Messaging Accounts in Empathy

The first time that you start Empathy, it displays the dialog shown in Figure 10-2, which provides multiple ways for you to configure how you use Empathy:

- Yes

# Chapter 10: Sending and Receiving Instant Messages

- Yes, I'll enter my account details now: Displays a dialog in which you can manually enter information about one or more instant messaging accounts.
- No, I want a new account: Enables you to create a new instant messaging account on instant messaging services that support remote account creation. Currently, only Jabber enables remote account creation — AIM, Yahoo, Google Talk, and so on require that you create an account via their web sites.
- No, I just want to see people online for now: Enables to define a People Nearby account, which is a local Empathy account that you can use to communicate with other people on your local network who are running Empathy and have this feature enabled.

FIGURE 10-2

# Configuring Empathy accounts

![](img/1a233c34336fbf5a85d6eb785e401709_402_0.png)

The next few sections explain the dialogs and procedures associated with each of these options.

# Importing Pidgin Accounts

If the "Yes, import my account details from" option is available, make sure that its radio button is selected and click forward to proceed. A dialog like the one shown in Figure 10-3 displays.

Make sure that the checkbox to the right of each of the accounts that you want to import is selected, and click Forward to proceed. Skip ahead to the section entitled "Seeing People Online Nearby" to proceed.

# Defining Existing Accounts Manually

If the "Yes, import my account details from" option shown in Figure 10-2 is not available or you do not want to import your Pidgin accounts and you already have instant messaging accounts
