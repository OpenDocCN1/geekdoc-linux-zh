
# Part III
## Getting Down to Business
### The 5th Wave By Rich Tennant

![](img/8dd43d91b80664e771e0c0a824d7392d_156_0.png)

"...and here's me with Cindy Crawford. And this is me with Madonna and Celine Dion..."

# In this part . . .

When you’ve had the guided tour of KDE’s features and capabilities, the next item on the agenda is to take it for a spin on the Net. Before you lift off for cyber-space, this part gives you a preflight check-out. It walks you through getting connected, using KDE on the Internet, sampling the applications and utilities that are available for use with KDE, and playing (or working) with non-KDE applications in a socially acceptable manner. So work it on out . . . or have fun . . . whichever.

# Chapter 8
## Getting Connected

### In This Chapter
- Getting an account with a Linux-friendly ISP
- Configuring a Linux account
- Tinkering with your modem
- Hooking up with an Ethernet connection
- KDE's network utilities: quick troubleshooters

After you have KDE set up and configured just the way you like it, you may want to start using your computer for things besides tinkering with the desktop. At the very least, you probably want to connect to the Internet, whether it's to download more neat KDE stuff or to share your joy about your new desktop with friends and strangers alike.

The KDE connection process is simple for Linux users who have already connected their machines to the Internet. If you are one of those already connected, skim through this chapter and confirm that your settings are correct. Unless you have some unexpected connection problems, though, feel free to jump off to the end of this chapter, where we cover Ethernet and some basic network diagnostic tools.

![](img/8dd43d91b80664e771e0c0a824d7392d_158_0.png)

If you've never connected your Linux machine to the Internet, you have some work ahead of you. Luckily, it's a pretty straightforward process; just remember to complete all the steps. You also have to get in touch with your current *Internet Service Provider*, or *ISP*, to see if it supports Linux or other UNIX-based operating systems. Many don't, including America Online. You'll probably have better luck looking for a smaller regional or local ISP than for one of the HumongolSPs that are clearly targeted at Windows users.

Connecting your computer to the Internet requires a couple of things.
- A **modem**, the piece of hardware that uses your phone line to transfer information between your computer and another computer.
- An account with an **Internet Service Provider (ISP)**.
- A working installation of KDE.

Sure, you can get on the Internet without KDE, but one of the tools that KDE gives you is called Kppp, and it’s a fast and flexible way to get all of those components talking with each other so you can get online. Kppp takes the information you give it about your ISP and your modem and sets up your computer to use that information so that you don’t have to think about it.

Kppp is another way in which KDE makes your computing life easier and simpler. All you have to do is type some stuff in, and KDE does the rest of the work. Not bad!

## Ready, Get Set...

What does it take to be Linux friendly? The most basic requirement is that the ISP permits its users to connect via UNIX-based operating systems and software. Beyond that, a Linux-friendly ISP should give its technical support staff some Linux training basic enough to answer those frantic “What do I do NOW?” calls. It’s nice to have Linux-specific FAQs available on the company’s Web site. Many ISPs use proprietary software (like AOL or MindSpring); make sure that it’s not required, because it’s almost always available only for Windows or Macintosh.

> We assume that you already have an account with an ISP that is at least Linux aware, if not downright Linux friendly. If you haven’t gotten that far, take a look at this chapter’s “Do you speak Linux here?” sidebar. We’ve consolidated some of the basic questions you should ask an ISP about its Linux friendliness.

You really don’t want to have the experience that we once had when calling a local ISP with a login problem. The tech support person said, “But you can’t use Linux to connect to our system! We don’t permit it!” (He was confused about the difference between permitting access from Linux users and supporting access from Linux users.) That was an odd response, given that probably half the ISP’s user base was composed of hardcore UNIX sysadmins, and it’s the sort of answer that sends chills down the spine of a newer Linux user with a question.

## Do you speak Linux here?

Finding a Linux-friendly (or at least Linux-compatible) ISP can sometimes be a tricky process. Living near a major metropolitan area may or may not be helpful. Most of the major national (and international) ISPs are really slanted toward the Windows user: they use proprietary software that's released in Windows format and that may make it difficult for even Macintosh users to get a compatible copy of the software.

However, many of the mega ISPs — including EarthLink, MindSpring, and WorldNet — claim to be open to Linux users. If you like the reliability of a major corporation and the freedom to move around the country without losing local dial-up numbers, you may want to look into accounts with the large ISPs. The major drawback is likely to be on the tech support end; if you call WorldDominator.net's tech support line with a problem, the one person who knows Linux may be on break. In the worst-case scenario, the tech support person may even insist that the ISP doesn't support Linux. Because a massive majority of their customers use Windows, there isn't a pressing need for the large ISPs to offer Linux-specific support.

Before you decide to go with a major corporate ISP, take a look at your local options. You may find happiness with a small ISP that's run out of an office park a few miles away and is based on Linux or a newer UNIX-based operating system. There, you may not compete with hundreds of thousands of other users for tech support. Check out some Linux-friendly ISPs at http://howto.linuxberg.com/isp.html.

> **WARNING!**
> You may not have very good luck convincing an ISP to be Linux friendly if it's running Windows NT. We aren't saying this just to Windows-bash; it's a serious philosophical difference that you need to consider when looking for an ISP. Companies that choose NT as their main operating system have deliberately chosen not to run UNIX or a UNIX-based operating system; you may be better off looking for a non–Windows NT ISP if one is available in your area.

When you've selected three or four possible ISPs, start making some phone calls or sending some e-mail. Ask each ISP the same questions, and then compare the answers when you're done phoning around. Here are some basic questions to ask:
- Do you support Linux?
- Do any of your users use Linux? How many?
- Do you have support materials written for Linux users?
- Are your technical support personnel trained to answer questions about your service from Linux users?
- Are your accounts normal PPP accounts? (That is, can I use any programs designed for use with a regular PPP connection?)
- Do you use any proprietary protocols or software? Are they required?

After you are hooked up with a good ISP, it’s time to get your connection going. Get some basic information together in front of your computer, so that you don’t have to search in the middle of the process. You need nine pieces of information:
- Your login ID, also known as your *username*.
- Your account password.
- The phone number your computer will dial to access the ISP.
- The authentication type used by your ISP, if it uses authentication.
- How your ISP assigns IP numbers: static or dynamic. If your ISP assigns static IP numbers, you need your IP number and the subnet mask.
- The IP numbers of the DNS servers.
- Gateway information. (You probably won’t have specific numbers for this section, because ISPs often shift gateway functions from machine to machine. See the numbered steps in the next section for more information about gateways.)
- The device name of your modem. (This should look something like /dev/modem or /dev/cua1.)
- Whether you need to use hardware or software flow control.

Confused yet? Don’t worry. Your ISP probably has most of this information typed up for you already: it’s either in the sign-up material you received, or it’s available on their Web page. (Obviously, it’s kind of hard to go to a Web page if you’re not connected to the Internet yet, but representatives can tell you this stuff over the phone or via fax as well.) All these terms are defined as configuring your connection is described.

## Plugging in your information

Now that you have everything together, it’s time to get started.

![](img/8dd43d91b80664e771e0c0a824d7392d_161_0.png)

The configuration process is filled with acronyms and numbers. Make sure you type everything into the text boxes exactly as they’re written on your information sheets. Use the same capitalization and dot placements. Otherwise, you’ll have to do all of this again, and you have better things to do with your time!

![](img/8dd43d91b80664e771e0c0a824d7392d_161_1.png)

- Open the KDE menu and select Internet::Kppp.
- To open the KDE menu, click the button with the KDE logo in the panel. The KDE menu pops up, from which you can select your choices. For more information on using the KDE menu, see Chapter 1.
- The Kppp dialog box appears, as shown in Figure 8-1. Kppp is the handy KDE way to configure PPP connections. PPP (Point-to-Point
