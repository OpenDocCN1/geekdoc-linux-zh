
## Using PPP for Dialup Connections

## Chapter 8

### IN THIS CHAPTER

- Obtaining a PPP Account 186
- Configuring Your Serial Ports 188
- PPP Authentication 193
- Creating PPP Scripts 195
- Using a GUI PPP Dialer 199
- Setting Up Dial-on-Demand for Automatic Connections 203
- PPP Problem Solving 206
- Summary 211

Even if you’re setting up a substantial private network, you might need to use a modem to connect to an Internet service provider (ISP). Perhaps your needs for Internet connectivity are modest, or faster forms of access aren’t available or are too expensive in your area. Whatever the case, Point-to-Point Protocol (PPP) is the usual means of connecting a single computer to the Internet via a modem.

### Note

PPP can also be used to connect two computers via a null modem cable—a cable that connects one computer’s outgoing lines to another’s incoming lines and vice versa. This can be a useful technique to connect PPP-enabled devices such as palmtop computers to a Linux computer. If the Linux computer is connected to the Internet, and if it’s configured for routing or IP masquerading, you can even give your palmtop full Internet access in this way.

Setting up a PPP link involves many of the same issues discussed in Chapter 7, “Setting Ethernet Options.” You must have an IP address for your computer and know the IP address of a router/gateway and DNS servers, for instance. As with Dynamic Host Control Protocol (DHCP; p. 179), PPP can automatically set some, but not all, of these options. Of particular importance, PPP links normally use dynamic IP addresses, meaning that your IP address changes from one connection to the next. This means that PPP isn’t normally a suitable protocol if you want to run a server for the outside world on your computer. Of course, you can run servers for an internal network and still connect to the Internet with PPP.

## Obtaining a PPP Account

The first step in connecting your computer to the Internet via PPP is to obtain an account with an ISP. You can check your local phone directory under Internet services or possibly computers for such listings. The Boston phone directory has five pages of listings for ISPs, and other major metropolitan areas are likely to have a similar quantity. If you have Internet access through some other means, you can check http://thelist.internet.com or http://boardwatch.internet.com/isp/ac/index.html for ISP listings; or you can try a Web search engine such as http://www.yahoo.com. Most colleges and universities and many companies provide dialup access to their students and employees, so you might be able to use such services if you want to connect your home LAN to your employer’s network.

Assuming that you want to use a conventional ISP, you might want to consider several criteria when selecting one:

- Size—ISPs vary in size, ranging from small operations run from an individual’s basement to international corporations. You’re likely to get the best customer support from a small company—for example, the owner of one small ISP made a house call to help configure a system belonging to a friend of mine! On the other hand, the larger organizations may offer free dialup access from anywhere in the country, and possibly the world, which can be a great boon if you travel or expect to move soon.

- Connection speeds—As of late 1999, the fastest theoretical speed for telephone modems is 56kbps (downstream; it’s slower upstream), achieved with the v.90 protocol. The earlier proprietary X2 and K56Flex protocols also achieved this speed, but they’re fading fast. I recommend that you only deal with an ISP that supports v.90 (other protocols are a bonus), even if you have a modem that can’t make the most of the available speed.

- Additional connection options—An increasing number of ISPs are offering access via dialup modems, Integrated Services Digital Network (ISDN) lines, Digital Subscriber Line (DSL) connections, and sometimes other methods. If you think you may want to upgrade your connection speed in the next few months, try to find an ISP that does or will support the technology you expect to use in the future.

- Number of modems—Some ISPs don’t have enough modems to cover the demand for their service. This results in busy signals when you call at popular times of day, such as weekday evenings. ISPs are often reluctant to admit to such problems, of course, but if you can obtain a dialup phone number, you can test availability by making a call or two each day for a week before signing up. You don’t even need a modem; just call the number and hang up when you hear the modem tones—or a busy signal.

- Services—Most ISPs offer one or two email accounts, access to a news server, and a certain amount of space for personal Web pages, in addition to raw Internet connectivity for Web browsing, FTP downloads, and so on. ISPs differ in how much of each of these things they offer, though—some give you more email addresses or space for Web pages, for instance, whereas some limit your total monthly online time. Some have special business accounts for large Web pages, even including hosting of a Web site under your own name, such as www.yourcompany.com. You’ll need to evaluate how well the available services suit your needs—and your budget.

- Linux friendliness—Many smaller ISPs run their systems using Linux or FreeBSD, so it may be surprising that most don’t list these operating systems (OSs) as being supported. In most cases, you can still use the ISP’s services with Linux; the ISP just won’t help you configure your system for PPP. Some ISPs are actively hostile toward Linux, or have systems that require you to perform unusual steps to connect using Linux. I once tried a large ISP but dropped it during the trial period because I couldn’t get this ISP’s servers and Linux to talk to one another, though I could connect fine from Windows and OS/2.
