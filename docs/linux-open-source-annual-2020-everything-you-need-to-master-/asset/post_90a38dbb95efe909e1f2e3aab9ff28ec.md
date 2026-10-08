
own really cool search syntax), but you can blacklist folders from the Settings > Desktop Search area. Even if previously indexed files have been securely deleted – with the shred command, for example – the metadata left behind by these trackers could provide valuable clues to a determined investigator.

The Vaults feature in KDE Plasma has been around for some time, but is easily overlooked. It enables you to encrypt folders and open them directly from the Dolphin manager (with the appropriate credentials, of course). There’s even a ‘paranoid’ mode which will forcibly disable all network access while a given Vault is open. You can check out Vaults and other cutting-edge Plasma joy with KDE neon 5.16.

![](img/7a0a282248f9658f0c87e55744c797b6_54_0.png)

# Internet of Terrible Things

Shadowy agencies snooping up data from the wire is one thing; being silently coerced into an ecosystem where you volunteer data to advertisers is another. From a privacy point of view, an even worse thing is the world of voice assistants such as Amazon’s Alexa, Apple’s Siri and Google’s imaginatively titled Assistant.

In April, Bloomberg revealed that Amazon employs a small army of low-paid humans spread across Boston, Romania and India to aid the machine-learning process. Their mission is to annotate recordings and very often, thanks to devices over-hearing their wake word, these people are getting entirely unintended glimpses into Alexa users’ private lives. Pretty creepy. In all likelihood Apple and Google do exactly the same thing – machine learning does some help, though not all.

Besides that issue, all your audio searches and textual transcriptions are held by the companies. They offer an option to ‘delete’ them, but that just dissociates the recording from the account: the recording itself still lives on as part of a massive vocal corpus. If you must use a Voice Assistant, we recommend the open source Mycroft, as featured in LXF249. Microsoft doesn’t store any data on its servers unless you specifically opt in. That voice data, Mycroft pledges, will only be used to improve the product, not sold on to advertisers.

IoT devices, even open source ones, can be hacked through – and thanks to poor design choices, regularly are. With that in mind the idea of showing a network stack in your fridge, front door or first-born doesn’t seem so hot. All of these things suffer from unprecedented glimpses into their users’ lives, quite literally in the case of home security cameras. Smart utility meters claim to save you money, but what good is that if they can be hacked?

![](img/7a0a282248f9658f0c87e55744c797b6_54_1.png)

If you must have a voice assistant it may as well be an open source one such as Mycroft, but consider turning it off when it’s not needed.

MAT in Tails is not much to look at, but you don’t need to look cool to stay covert. And no, you can’t see our camera’s serial number, damn it.

# Email Privacy

In this world of Slack and Discord and Telegram and whatever other communication platform is currently hip, it’s easy to forget about humble email. Email is pretty special in that it’s federated – you don’t need to be the same email provider as the person you’re talking to – and decentralised: it can be your own provider, if you can understand Postfix. These are ideas that are recently coming back into fashion. It’s also very old, and when it was invented there was very little thought given to security. As late as the turn of the millennium, most SMTP servers didn’t require authentication (days were the glorious old days for spammers) and even today some email is transmitted in the clear.

Thankfully this fraction is very much a minority thanks to widespread adoption of STARTTLS, which encrypts communication between relays. It’s still necessary for relays to see the messages passing through them, so from the point of view of someone who doesn’t want their messages intercepted, it’s best to encrypt them at source using PGP email. Confusingly, this is done on Linux using GPG, which we’re not going to try to explain here.

Fortunately, Thunderbird on Tails includes the Enigmail plug-in which makes public key cryptography as easy as it can be. Note that even if you figure this out, email headers are still visible to relays involved in message delivery, and this is precisely the kind of metadata that spooks would love to harvest.

![](img/7a0a282248f9658f0c87e55744c797b6_54_2.png)

CREDIT: mycroft.ai

# Going to Ground

Use Tor and Tails to hide your browsing, and then upset the UK ISP Association by enabling DNS-over-HTTPS, villainous stuff!

![](img/7a0a282248f9658f0c87e55744c797b6_55_0.png)

> Every three months linuxformat.com has to get a new SSL certificate so that our viewers can continue to see this friendly green padlock.

Thanks in large part to the efforts of Let's Encrypt over the past few years, most websites are now served over HTTPS. This provides two things: authentication and privacy. Authentication in the sense that you can be sure that the website you’re looking at isn’t some kind of forgery, and privacy in the sense that communication between you and the webserver is encrypted.

As such, HTTPS more or less thwarts the ability of a passive middleman to see which pages are being viewed, but out of technical necessity your DNS provider – usually your ISP – needs to see the domain name, and your ISP needs to see the IP address it resolves to. You can, and in a lot of cases should, use a VPN, but that just shifts the second requirement downstream. Also, there’s generally very little reason to trust a VPN any more than you do your ISP – unless your ISP is really bad, in which case you should find another one. You can use one of any number of public DNS servers like Google’s 8.8.8.8 or Cloudflare’s 1.1.1.1 which remove your ISP from the equation altogether – except that ISPs then have a nasty habit of intercepting (DoH!-Ed) DNS queries.

Multiple websites are often hosted behind the same IP address, and for this to work with HTTPS a scheme called SNI (Server Name Indication) is used. This requires the client to send the desired domain name to a server unencrypted, which means it can be eavesdropped twice: once during the DNS look-up, and once again during the TLS handshake. If you don’t like this, there’s always the Tor network, but that’s slow in comparison to regular browsing, and just downloading the Tor Browser is likely to score you a space on a very big list at one or more of the three-letter agencies.

Nonetheless, we love being on lists, so we’ll show you how Tor works just over the page.

Work to solve hostname leakage is underway in the form of ESNi, which you can read more about at Cloudflare’s blog (https://blog.cloudflare.com/ encrypted-nsi), who are leading this charge. ESNi requires changes to be standardised by browsers before it works, and is a moot gesture so long as DNS queries are still unencrypted. But there is a solution to that DNS problem – two, in fact: DNS-over-HTTPS (DoH) and DNS-over-TLS (DoT). For the purposes of atrocious journalistic oversimplification, let’s say that these two are similar, but that DoH looks like regular web traffic so is much harder for ISPs to filter.

DoH can be implemented in a number of ways. We talked about using DNSCrypt-proxy in our Harden Mint feature in LXF247. If you missed it, that sets up a local DNS server that takes regular DNS queries and proxies them to an external resolver, one that supports DoH – or the eponymous DNSCrypt protocol, which we won’t cover here. However, since we wrote that DNSCrypt 2.0 has become the standard, and unfortunately it hasn’t made it into the Ubuntu 18.04 LTS repos (it’s in 19.04 though). So if you’re using the LTS you’ll need to use Andrei Shevchuk’s PPA to get the newer version, which is a matter of:

```
$ sudo add-apt-repository ppa:shevchuk/dnscrypt-proxy
$ sudo apt update
# Then it can be installed with:
$ sudo apt install dnscrypt-proxy
```

We can then point our DNS queries to our local resolver via NetworkManager. To do this, go to the Settings screen and find your wired or wireless network. If the Method drop-down is set to Automatic, change it to ‘Automatic (Addresses only)’, which will still use DHCP to request an IP address from your router, but will ignore what it (and your ISP) tells you to use for DNS. In the DNS box enter 127.0.2.1 – the address DNSCrypt runs on – and then restart your network by disconnecting and reconnecting. You can check that these settings have taken effect by visiting one of any number of DNS-leak test websites. Many of these will

![](img/7a0a282248f9658f0c87e55744c797b6_55_1.png)

NetworkManager integrates nicely with OpenVPN, so connecting to a commercial VPN is often just a matter of importing an OVPN file.
