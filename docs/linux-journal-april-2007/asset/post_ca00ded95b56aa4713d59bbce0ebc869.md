
Enlightenment as the theme and find that Firefox is already conveniently installed. Even better, the system has by default correctly found my DHCP server and configured itself so that I’m on-line and ready to go.

## Surf the Net in PlayStation 3 Linux

Now, I can start to analyze whether the YDL installation is actually a configuration that addresses my earlier stated needs for a software solution that makes the PS3 a useful Internet machine, and a quick visit to [linuxjournal.com](http://linuxjournal.com) confirms that, yes, it works fine, it’s darn fast and eminently usable. Nice!

One of the sites I use as a test is Google’s Gmail service. It’s complex behind the scenes and quite powerful, so the question is always whether it works and renders properly on a new system. YDL came through like a champ, working just fine and letting me navigate through my e-mail securely through Firefox. Thunderbird is also pre-installed and ready to go, and configuring a POP3-based e-mail account is pretty straightforward for most Linux users, so there are at least two good avenues for accessing your e-mail.

![](img/3c4d8a97b5d96c835281dc0dacbc8551_74_0.png)

Figure 5. Testing Google’s Gmail with YDL

That means, of course, that YDL does indeed meet my primary criteria for usability, letting me surf the Web and interact with my e-mail, all from the comfort of my easy chair and with a simple USB keyboard added onto my sleek PlayStation 3 device.

But, Linux offers a lot more capability, and as an experiment, I launched Rhythmbox and quickly concluded that I have had my expectations of music players really screwed up by using iTunes for so many years. It’s astonishing to me that I can choose “Internet radio stations” and not get a list of available stations, but instead have to figure out the URL of the station I desire so I can “tune in” to it. Unfortunately, all these years into the Linux evolution, and there are still too many apps that rough around the edges like this.

I went to Firefox, searched for “internet radio station jazz”, found one through the popular Live365 site, selected the channel, had it try to download a streaming file that caused the launch of the Helix player, only to find that it doesn’t have the capability of playing back that type of content. Next stop: AccuRadio, but I wanted me to install a new plugin. Yeh, New Orleans Jazz channel WWOZ offered up a URL, so I pasted that into Rhythmbox just to find it didn’t work either. To heck with it! How is someone like my Mom supposed to survive so much hassle to get audio in YDL?

## At the End of the Day, It’s a Linux System

As I expected, it may be slick and fast running on the Sony PlayStation 3 with its powerful Cell processor system, but it’s still the same Linux that we’ve gotten used to with no exciting new capabilities, no easier way to work with the various media on the Web, and the same round edges I’ve been bothered by for over a decade now.

Unlike most Linux systems, however, YDL on PS3 at least lets you reboot and go back into the world of the PlayStation, where you can easily run photo slideshows, upload and enjoy your music library, watch DVD and Blu-ray HD video and, of course, play some of the amazing games available at boot time too.

Really, it’s one heck of a combination, and if you know someone who would like to have access to all the power and capabilities of the Cell processor through Terra Soft Solution’s YDL system, along with the fun and power of the PlayStation 3, it’s really one heck of a combination. Even if you just want to hack, it’s cool to have a foreign OS on the system as an option at boot time too.

> Dave Taylor has been poking around in UNIX and Linux since the mid-1980s and has contributed various software to its evolution. He has run Linux on all sorts of strange devices now, including his tri-booting Mac laptop and Sony PlayStation 3. He also runs a busy Q&A and trouble-shooting site ([AskDaveTaylor.com](http://AskDaveTaylor.com)) and has written a number of popular tech books, including *Growing Your Business with Google* and *Wicked Cool Shell Scripts*.

![](img/3c4d8a97b5d96c835281dc0dacbc8551_74_1.png)

## The OpenSSH Protocol under the Hood

The nitty-gritty details as to what OpenSSH is and why it is ubiquitous.

GRISH VENKATACHALAM

Is there a program more commonly used in day-to-day Linux computing than SSH? I doubt it. Not only is it rock-solid, secure and versatile, but it also is extremely simple to use and feature-rich. Because its algorithms and protocols are both state of the art and their implementation is open for peer review, we can rest assured on the cryptographic integrity of SSH. SSH does have weaknesses, however, although most of them stem from social engineering, and working around broken protocols, such as X11, pose a big challenge.

SSH can do wonders in only a few lines of C code—thanks to the UNIX philosophy of stringing together powerful tools in generic ways.

SSH acts as a secure channel, and it makes a remote system appear local, and a local one appear at the remote side. It can be used either for remote command execution, with or without a pty, and it can be used for multiplexing several TCP and X11 sessions. It also can be used for tunneling insecure protocols, such as POP3 or SMTP, through secure SSH tunnels. In addition, it can be used with some limitations to tunnel FTP securely.

## The OpenSSH Architecture

Let’s begin with the overall scheme of things.

As shown in Figure 1, OpenSSH is composed of three key layers. The bottom layer, ssh-transport, is the most critical component involved in all the crypto operations, such as key exchange, re-keying at intervals, protecting against attacks in various ways and so on.

The layer on top of ssh-userauth, is responsible for authenticating end users to the sshd daemon that runs at the server end. Remember that SSH authenticates both ways. The client SSH program authenticates the sshd server daemon using the ssh-transport protocol. After authentication, key exchange is completed, and a secure connection is established. Subsequent to that, user authentication takes place.

ssh-userauth provides a lot of flexibility, because users can authenticate to the server in various ways—from a private key on a smart card to simple user name/password authentication. Once it goes through, the ssh-connection layer establishes a secure channel, either for executing a remote command or to obtain an interactive login shell.

The ssh-connection layer is capable of multiplexing any number of simultaneous independent secure sessions over a single ssh-userauth layer with the transport stack layer below it, as shown in Figure 1. All of SSH’s magic—forwarding arbitrary TCP ports from local to remote and remote to local, acting as a SOCKS proxy, forwarding X11 connections, establishing VPN tunnels, executing remote commands with and without a pty—is done with the ssh-connection layer.

SSH has flow control built in to the protocol. Each secure channel has a separate window size allocated. Because SSH operates above a reliable TCP layer, this does not have much of a role. At least, it is not as critical as the TCP windowing mechanism. Most of the critical channel open/close messages and other termination messages don’t consume any window space.

![](img/3c4d8a97b5d96c835281dc0dacbc8551_75_0.png)

Because all messages are encrypted and integrity protected, nobody can interpret the messages. There is a special LMSG_IGNORE message type that can be used for defaulting traffic analysis attacks. These are the kinds of attacks that figure out when data is going over the wire and how much data is being transferred.

SSH, of course, comes with many other niceties for sending secure KEEPALIVE messages, redirecting stdin to /dev/null for specialized X window applications and many more.

Now, let’s take a look at a sample SSH session and typical message exchanges (Figure 2).

Here is a typical unencrypted SSH packet:

| Byte | Description | Type | Recipient Channel | Value |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Type | SSH_MSG_CHANNEL_REQUEST | | |
| 4 | Recipient channel | uint32 | | |
| 1 | Request type | string | "pty-req" | |
| 1 | Want reply | boolean | | |

