![](image_rsrcYC.jpg)

Table of Contents

[Preface](#part0002.xhtml)

[Is Tor Safe in 2022?](#part0003.xhtml)

[Tor Risks](#part0004.xhtml)

[Exit Nodes](#part0004.xhtml_aVP)

[Intelligence Agencies](#part0005.xhtml)

[Quantum and FoxAcid System](#part0005.xhtml_aWK)

[Tor Step-by-Step Guide](#part0006.xhtml)

[Tor Installation](#part0007.xhtml)

[What Tor Cannot Do](#part0010.xhtml)

[Tor Apps & Anti-Fingerprinting Tools](#part0011.xhtml)

[Orbot](#part0011.xhtml_aVA)

[Invisibox](#part0011.xhtml_aW1)

Text Secure

[Google and Tor](#part0012.xhtml)

[Captchas](#part0013.xhtml)

[SpiderOak](#part0014.xhtml)

[Tails](#part0015.xhtml)

[Tails Limitations](#part0016.xhtml)

[Chrome](#part0017.xhtml)

[User Agent Switcher](#part0017.xhtml_aV8)

[CanvasBlocker](#part0017.xhtml_aWF)

[Deadly Firefox Options](#part0018.xhtml)

[Whonix & Tor](#part0019.xhtml)

[Torbirdy](#part0019.xhtml_aVC)

Macchanger

[Whonix Bridges](#part0020.xhtml)

[Using Your Real Name Outside of Tor](#part0020.xhtml_aV4)

[Email Anonymity](#part0021.xhtml)

[Guerrilla Mail](#part0021.xhtml_aW3)

[PGP](#part0021.xhtml_aVJ)

[Mymail-Crypt](#part0021.xhtml_aVX)

[Freenet](#part0022.xhtml)

[Frost](#part0023.xhtml)

[Passwords & Tor](#part0024.xhtml)

[Changing Passwords](#part0024.xhtml_aVG)

[Storing Passwords in Tor Browser](#part0024.xhtml_aWY)

[Preventing Non-Tor Activity From Being Linked with Tor Activity](#part0024.xhtml_aWR)

[Keyloggers](#part0025.xhtml)

[Signs](#part0025.xhtml_aW4)

[Software Keyloggers](#part0025.xhtml_aUG)

[Hardware Keyloggers](#part0025.xhtml_aX1)

[Keylogger Prevention](#part0025.xhtml_aVS)

[Anti-Keyloggers](#part0025.xhtml_aWB)

[Darknet Markets](#part0026.xhtml)

[Fraud Prevention](#part0027.xhtml)

[When It Is Okay to FE (Finalize Early)](#part0028.xhtml)

[When It Is NOT Okay](#part0028.xhtml_aVM)

The Long Arm of the Law

How Most Get Caught

[Darknet OPSEC](#part0029.xhtml)

[On Running a Hidden Tor Server](#part0030.xhtml)

[Tor and Your PC](#part0030.xhtml_aV3)

[Situation Awareness](#part0030.xhtml_aUC)

[Darknet Personas](#part0031.xhtml_aU9)

[Tor Hidden Services](#part0032.xhtml)

[The Death of Anonymity](#part0033.xhtml)

Conclusion

Preface

You want what you want.

Invisibility. Anonymity. Ghost protocol.

You've taken the red pill and have seen the truth, and you don't like it. I don't blame you. I didn't like it either. But what I thought I knew about Tor and other incognito tools was only a drop in the ocean next to what's really out there. Stuff you don't find on many tech forums. They're whispered in private, of course, but it's all invisible to you. Until now.

Which brings us to you and I, or rather what I can do for you. It's amazing what a guy can learn in a decade when he rolls his sleeves up and gets his hands dirty. Private hacker forums. Usenet. Freenet. I scoured them all for years and what I've learned isn't anywhere else on Amazon.

Equally amazing is what you can learn for a few dollars in a weekend's worth of reading. That's me, and soon to be you. Where you will be by Monday is where I am now, only without the years of mistakes. Mistakes I made using Freenet, Tails, PGP. You name it, I did it. And boy did I make BIG ONES. Those are mistakes you'll avoid because, after you've read this guide, you'll know more than 85% of the Tor users out there, and know more about anonymity than most Federal agents. Even the so-called superhackers at the NSA who only get by with a minimum amount of work every day, mostly involving eradicating your right to privacy.

To that, if you don't come away satisfied, return it for a full refund.

But I know you won't. Because once you've taken the red pill, there ain't no going back. You can't unlearn what you've learned, unsee what you've seen, and you'll want more. Much, much more.

First off, we're not sticking with the basics here. If all you want is Tor for Dummies, look elsewhere. Where we're going is dangerous territory. It's shark territory when you get right down to it. But don't worry. We've got shark repellant and everything you need to surf safe. You'll reap benefits you've only dreamed of and by the time we're done, you'll have gained NSA-level anonymity skills with a counter-surveillance mindset that rivals anything Anonymous or those goons at the NSA can come up with. They won't have a clue as to how to find you.

Secondly, for a few dollars, you'll know every exploit those superhackers like to wield against Tor users and more: How to avoid NSA tracking. Bitcoin anonymity (that is, real Bitcoin anonymity), Opsec advice, Darknet markets and Darkcoins and, well... frankly it's a very long list, and by the time you're done you'll be a Darknet artist when it comes to marketplaces and buying things cloak and dagger style.

Third, we'll go over many techniques used by the CIA and FBI to entrap users. False confessions. Clickbait. Tor honeypots. It's all the same when you get right down to it. You'll learn the same techniques used to catch terrorists, hackers and rogue members of the hacker group Anonymous and couriers for Reloaded. Baits and lures and how to spot an LEA agent from a mile away. I break it all down into simple steps that you can understand. A few dollars for this info will save you a LIFETIME of grief. And no, you won't find it on Reddit or Ars Technica or Wired. If you're mulling this over, don't. You need this now. Not when you're framed for something you didn't do.

Fourth... reading the dangerous material herein requires you take ACTION. The Feds take action. Identity thieves take action. Hackers take action. Will you? You have to take action if you want results. What you're glossing over right now is no mere guide. It's a mindset. It's professional level stuff meant to keep you and your family safe for a decade out, going far beyond apps and proxies and it's all yours if you do two simple things: Read, then act. Simple. Because you know what they say: Knowledge is power.

No, strike that. Knowledge is potential power. Your power. But only if you act.

Fifth... I update this book every month. New browser exploit in the wild? I update it here. New technique for uncloaking Tor users? You'll read it here first. We all know how Truecrypt is Not Safe Anymore, but that's only the beginning. Besides, freedom isn't free.

Lastly... The scene from Jurassic Park with Dennis Nedry, I believe, is a nice frightful analogy to what happens if you don't take your security seriously. We see poor Dennis try to get his jeep out of the muck in the middle of a tropical storm. Lightning unzips the sky and the rain pours. The thunder rolls. A dilophisaur bounds upon him, beautiful and appearing curious. Yet boiling under his head lies a deadly secretion as it sniffs the air and cocks it's head at Nedry - moments before spraying his chubby eyes with poison. Blinded, he staggers back to the safety of the jeep, wailing and gnashing teeth, only to discover a visual horror to his right: he's left the passenger-side door ajar - wide enough to let Mr. Curious in for a juicy evening meal, which it savors with a row of piranha-sharp teeth.

The point is this: Don't be Dennis Nedry. There are far bigger creatures who'd like nothing better than to split your life (and family) wide open if for no other reason because THEY CAN. Such is the nature of the elite.

Unless, of course, you tame them...

![](image_rsrcYD.jpg)

Which is not bloody likely.

Is Tor Safe?

That seems to be the question alright. As to what the true answer is, it really depends on whom you ask, because there are always wolves in sheep's clothing out there who stand to gain from your ignorance. Many say no. A few say yes. The media, for all their expertise in things political and social, come up woefully lacking when something as complex as Tor is discussed.

Case in point: [Gizmodo](http://gizmodo.com/hackers-who-shut-down-psn-and-xbox-live-now-attacking-t-1675331908) reported that a group of hackers managed to compromise enough Tor relays to decloak Tor users. If you're just hearing this for the first time, part of what makes Tor anonymous is that it relays your data from one node to another. It was believed that if they compromised enough of them, then they could track individual users on the Tor network and reveal their real life identities. Kind of like how the agents in The Matrix find those who've been unplugged.

Anyway as luck would have it, it turned out to be kiddie script-hackers with too much time on their hands who simply wanted a new target to hack. Who knows why. Could be that they'd toyed with the Playstation Network long enough and simply wanted a curious peak here and there. These were not [superhacker-level](http://www.slashgear.com/nsa-has-super-secret-hacker-collective-according-to-newly-revealed-snowden-docs-29295407/) NSA members, either.

But as is usually the case with the media, this attack attracted the attention of a few bloggers and tech journalists unsympathetic to Tor and frankly, ignorant of what really constitutes a threat. The Tor devs commented on it, too:

"This looks like a regular attempt at a Sybil attack: the attackers have signed up many new relays in hopes of becoming a large fraction of the network. But even though they are running thousands of new relays, their relays currently make up less than 1% of the Tor network by capacity. We are working now to remove these relays from the network before they become a threat, and we don't expect any anonymity or performance effects based on what we've seen so far."

What those conspiracy bloggers failed to report was that any decentralized network like Tor is a prime target for attacks such as the above. But to truly stand a chance at punching a hole through this matrix, hackers would need Tor to implicitly trust every new node that comes online. That just doesn't happen.

It also takes time for fresh relays to gather traffic - some as long as sixty days or more and the likelihood of being reported is rather high since the IP addresses are out in the open, which only speeds up malicious reporting. The real danger, and has been since inception, is scaring Tor users to less secure methods of communication. That's what the NSA wants. The CIA already does this in foreign countries. Now the NSA is following their lead.

The REAL Risk of Using Tor

I list them here before we dive deep into enemy territory so you'll know what to avoid before installation, and maybe get an "a-ha!" moment in subsequent chapters. As you read, remember that having Javascript on is really only a drop in the ocean next to what is possible for an enemy to kill your anonymity.

Javascript

It's widely known that leaving Javascript on is bad for a Tor user. Ninety-five percent of us know this, but the mistakes of the 5% get blown out of proportion and thrown into the face of the rest of us. Worse, many websites now run so many scripts that it seems as though they hate Tor users.

One site required over a dozen. Without it, the page was/is/will be pretty much gimped. Sometimes it's not even readable. You can imagine what might happen if you were using Tor and decided to visit that site if it were created to lure users into a honeypot. I recall one researcher claimed that "81% of Tor users can be de-anonymised."

Bull.

That 81% figure came about because the targeted users knew little about the NoScript browser add-on, and likely mixed Tor usage with their daily open net usage, providing ample data for a correlation attack. But that was just the icing on the cake. They left personal details *everywhere*; using the same usernames and passes they do elsewhere on the open net. Bragging about their favorite Netflix movies. Talking about local events (Jazzfest in New Orleans!). The weather (Hurricane in the French Quarter!). You get the idea. Much more on this later.

Volunteering as an Exit Node

Another doozy, though not quite the granddaddy of all risks. It's still risky. On the plus side, you as a valiant believer in anonymity graciously provide bandwidth and an "exit pipe" to the rest of the Tor users (hopefully none of whom you know) so that they may pass their encrypted traffic through your node. Generous? Certainly. Wise? If you live in the States... hale no, as my Uncle Frick in Texas used to say.

It isn't that it is illegal per se to do so. On the contrary, but what passes through your Tor node can land you in hot water if you live in a police state like my native Louisiana. All exiting traffic from your node (i.e. other people's traffic) is tied to your IP address, and as others have found, you put yourself at risk by what others on the other side of the planet do with your node.

Lots of new Tor users fire up BitTorrent that's been configured for Tor and suck down all the bandwidth. It makes for a very miserable Tor experience for other users. You may get served with a copyright violation notice (or sued), or perhaps even raided at 6 AM by a black party van if child porn ends up flowing out of your pipes. Think carefully and do your research before taking on such a risky charge, lest your computer be seized and your reputation ruined. Innocent men have gone to jail for their overconfidence.

Running an Exit Relay From Home

Running it from home is even worse then using cloud storage, and is infinitely more dangerous in the USA and UK than say, Thailand or Philippines. If the law for whatever reason has an interest in your Tor traffic, your PC may just be seized, yes, but that's only the start. In the UK, there are no 5th amendment protections against self-incrimination. Anywhere. A crusty old judge can give you two years just for not forking over the encryption keys. If they did have it, they wouldn't have bothered raiding your bedroom and spooking the bejeezus out of your cat at the crack of dawn.

We'll get into the nitty details later, but these are the Rules I've set for myself on occasion.

- Refrain from routing normal traffic through it

- Never do anything illegal (more on this later as it's a very grey area)

- Never put sensitive files on it (for ex., financial data, love notes, court documents, lawyer correspondence)

- Be as transparent as possible that I'm running a Tor exit.

Intelligence Agencies

They've declared war on Tor and its stealth capability. No doubt about it. And though they'll fight tooth and nail to convince you it's for your own good, really what it all comes down to isn't so much national security as it is national control: Control over you in that they can't see what you're doing on Tor. Nor do they know why. They don't like that.

It's pomposity on a galactic scale unheard of when you look at how much data they're siphoning from everyone's pipes. Every time some new revelation leaks out of Edward Snowden's mouth regarding the NSA, I think of the Gyro Captain from the Road Warrior film with Mel Gibson; the gangliest, sorriest excuse for a desert raider this side of the Fallout games (who's also frustratingly loveable). Said Captain tries to rob Mel of the gasoline that fuels his souped up Falcon Coupe V8\. Only it doesn't end well for him. In the attempt, the poor sod makes himself a slave, a delicious reverse slavery pact that ends up with him carrying Mel's gasoline cans across the desert and Mel's dog nipping at his filthy heels as he begs Mel not to ice him right there and then. In fact if it'd not been for the mercy Mel kindly bestowed, his theft  quite literally would have blown up in his face due to the custom bomb underneath the hood. Such a nice guy.

Well. The time for playing nice guy to the NSA is over. They spend so much money and waste so much time chasing you simply because they don't like you or your actions not being easily identifiable.

As you probably know, it's more costly to go after a high-value target. But they don't know if you are a high-value target or merely low-hanging fruit. As we've seen in the case of bored Harvard students, anyone can get into serious trouble if they go into Tor blind.

Even Eric Holder has publicly pointed out that Tor users are "non-US persons" until identified as citizens. They do this using two methods:

The Quantum and FoxAcid System

More on how to defeat this later, but here is the gist of it:

- Both systems depend on secret arrangements made with telcos.

- Both involve lulling the user into a false sense of security.

- Neither system can make changes to a LiveCD (Tails) (that's in our favor)

- Both can be defeated by adhering to consistent security habits.

Defeating this requires a mindset of diligence, and as you probably know, diligence is not compatible with procrastination. Therefore, you must resist the urge to procrastinate.

I say again. DO NOT procrastinate. Decide ahead of time to avoid risky behavior. We'll get to them all. A good, security mindset takes time and effort and commitment to develop, true enough, but should be nurtured from the very beginning, which is why the RISKS are placed up front, ahead of even the installation chapter. Things tend to drag in the middle of a book like this, and are often forgotten.

Speaking of risk, if you want to know what truly keeps me up at night, it's this question:

What do other nations tell high-level CEOs and intelligence agencies (Hong Kong, for instance)?

If the only thing I can trust is my dusty old 486 in my attic with Ultima 7 still installed atop my 28.8k dialup modem, then it's safe to assume every commercial entity is jeopardized by the NSA. And if that's true, if the NSA has to jump hoops to spy on us, how easy is it to infiltrate American-owned systems overseas with our data on those systems?

If no corporation can keep their private info under wraps, then eventually the endgame may evolve into a Skynet grid similar to the Soviet-era East/West block in which CEOs have to choose east or west. But that's like trying to decide whether you want to be eaten by a grizzly bear or a lion.

That's jumping the gun a bit, but at least now you know the real risks. The main ones, anyway.

Every one of these risks can be minimized or outright defeated using knowledge that is in this book. The sad part is that most readers will forget roughly 80% of what they read. Those who take action will retain that 80% because they are making what they've read a reality: Making brilliant chesslike countermoves when the NSA threatens your Queen. If you don't take action, but merely sit there waiting forever to make your move, you forfeit the game. They win. So don't be like a frog in a slowly boiling pot of water, because not only will you perish, but your future generations will as well.

Alright then. Enough about the risks. Let's get to it.

Tor Step-by-Step Guide

Now let's answer what Tor is and what it does and what it cannot do. You've no doubt guessed by now it's some kind of hacker's tool, and you'd be half right, but only from the perspective that a powerful tool like Tor can be used for just about anything. In fact anything can be bought (except maybe voluptuous blondes in red dresses) anonymously, as long as you're cautious in using it. Tor users who get cocky often get caught doing something illegal. Like insulting the king of Thailand or threatening the President of the USA with a pie to the face.

Before you criticize Tor, try to remember that it's not about buying drugs or porn or exotic white tiger cubs. It's about anonymous communication and privacy - with the main function being that it grants you anonymity by routing your browsing session from one Tor relay to another, in essence masking your IP address such that websites cannot know your real location. This gives the average pc user enormous power to act anonymously online.

This power allows you to:

-  Access blocked websites (Facebook if you are in China)

-  Access .onion sites that are unreachable via the open internet

-  Threaten the president with a pie-to-the-face...and no Secret Service visit!

It does all of this by a process called onion routing.

What's onion routing, you ask?

Think of it as a multi-point-to-point proxy matrix. Unlike peer to peer applications like BitTorrent or eMule which expose your IP to everyone, Tor uses a series of intermediary nodes (and thus, IP addresses) that encrypt your data all along the network chain. At the endpoint, your data is decrypted by an exit node so that no one can pinpoint your location or tell which file came from which computer. Due to this anonymizing process, you are anonymous on account of the packed "onion layers" that hide your true IP address. Hence the onion symbol of Tor.

It's even possible to build a site such that only Tor users can access it. Also called "Onion Sites," though technically challenging, you don't need a Ph.D in computer science to build one, or even a Bachelor's degree. You don't need to know how to code at all, in fact, and these Onion sites are unaccessible by anyone using the regular web and regular, non-Torified Firefox.

We'll delve deeper into that later, as well as how to construct a fortress of doom that nothing, not even the NSA, can penetrate.

Installation

Installing Tor is dirt simple. You can download it [TorProject.org](https://www.torproject.org/projects/torbrowser.html.en).

If your ISP blocks you from the Tor site, do this:

- Shoot an email to the Tor developers on their homepage. Tell them the situation. You can get an automated message sent back to you with the Tor installation package attached. That's the simple way.

- The harder way is to use Google. At the main page, do a search for any cached websites, including Tor, that might have the install package to download. Many tech sites may just have it cached on their servers in the event of all-out nuclear war. It's a 50/50 chance but I've found it useful for finding 'discontinued' or blocked applications.

- Get a friend to email you the Tor installation. Ask for Tails, too. Think of Tor as the nuclear weapon and Tails as the uranium that makes that pretty mushroom cloud in the sky. You don't need both, but it's always better to go the Tails route.

- VERIFY the signature if you obtain it elsewhere other than from the main Tor site, but for the love of all that is sacred and holy Threepwood, verify it even if your friend hand-delivers it. I've gotten viruses in the past from friend's sharing what they thought were "clean" apps. Believe me, in a situation where you fire up Tor to discuss nuclear launch codes, you don't want a keylogger mucking things up for you.

Now then. Choose Windows, Linux or the Mac version and know that your default Firefox install won't be overwritten unless you want it to. Both use Firefox, but Tor is a completely separate deal. You'll notice it has the same functions as Firefox: Tabs. Bookmarks. Search box. Menus. It's all here... except your favorite add-ons.

On that point, you might be tempted to install your favorite apps. Don't give in to that temptation. Multiple add-ons that do nothing for your anonymity might assist someone in locating you over Tor by what is known as "[Browser fingerprinting.](https://cryptostorm.org/download/file.php?id=1379)”

![](image_rsrcYE.jpg)

After installation, you should see the green welcome screen below:

![](image_rsrcYF.jpg)

Now you've got some choices. One is to volunteer your bandwidth, which makes it easier for other Tor users, but comes with risk.

After Tor is installed, every page you visit with the Tor Browser will be routed anonymously through the Tor network. There is, however, an important detail you need to know concerning security, and that is that your Tor settings are merely reasonable starting points. They are not optimal, and certainly not bulletproof. We're still at the infancy stage and quite frankly, optimal as Tor knows optimal is largely dependent on hardware (network, CPU, RAM, VM, VPN), and so each person's setup will be different just as a person's security needs in Tehran, Iran are different than in Montreal, Canada.

What Tor Cannot Do

Now for what Tor cannot do, or at least cannot do very well. In the future this may change, so don't fall on your sword just yet.

1.) Tor cannot protect you from attachments.

This isn't limited to executables, but anything that can be run by code. This means Flash videos as well as RealPlayer and Quicktime. Those babies can be configured to send your real IP address to an adversary. That's not good. So we must never run any executable or app unless we trust the source implicitly. If at all possible, go open-source. This also goes for any encryption scheme. Let's stop right there for a moment.

If you're going to use Tor, encryption is mandatory. It's not an option. I've heard some say on a few encryption blogs that it is, but that's like saying learning Thai is optional if you're going to live in Bangkok all year. You won't get far that way.

2.) Tor cannot run torrents well.

Old news, right? Thousands still do this, and I can understand why with how lawsuit-obsessed North America seems these days. Better safe than sorry, they claim. I've heard every excuse under the rainbow that using torrents on Tor is no big deal. The only problem is... they are safe and everyone else is sorry. Tor cannot do P2P apps like Emule and Limewire without making everyone else's Tor experience miserable. It simply sucks down too much bandwidth.

3.) Tor cannot cloak your identity - If you're tossing your real email around like Mardi Gras beads, or even if you give your true email on websites while using Tor, you should consider your anonymity compromised. Nuked. Eviscerated. Your virtual identity must never match up with your real-life identity under any circumstance. We'll delve far more deeply in later chapters on how to do this the right way, but know that those who ignore this rule get hacked, robbed, arrested, or mauled by capped gremlins with the letters 'FBI' on their jackets. Much more on this later.

Tor Apps & Anti-Fingerprinting Tools

A few applications, mobile and otherwise, make Tor less of a headache, but they're not particularly well suited for desktop users unless you're doing some kind of emulation. But with everyone using mobile these days, some of these have benefited me in ways I never thought possible. Be sure and read the comments in the Play Store since updates tend to break things.

Orbot: Proxy with Tor

This one is basically Tor for Android, which you can get at the Google Play store or at their homepage.

![](image_rsrcYG.jpg)

It is a proxy app that runs similar to the desktop app and encrypts your net traffic, as well as protects you from surveillance and fortifies you against traffic analysis. You can use Orbot with Twitter, DuckDuckGo or any app with a proxy feature. I've used this for a long time now and have gotten used to it's strengths

[Invizbox](https://www.indiegogo.com/projects/invizbox-privacy-made-easy) - Privacy Made Easy

![](image_rsrcYH.jpg)

Invizbox plugs into your existing router or modem. A new "InvizBox" wifi hotspot will appear. Connect to the new hotspot and follow the one time configuration set up and you're ready to go. All devices that you connect to the InvizBox wifi will route their traffic over the Tor Network. This isn't a required app, mind you, but it makes for simplifying things.

Signal Private Messenger

![](image_rsrcYJ.jpg)

This app encrypts every message on your mobile phone and is simple to learn. Better still, in the event you leave your phone at Marble Slab, rest assured your privacy is safe due to the encryption within. It's also open-source. To that, far too many applications aren't and thus cannot be peer-reviewed by anyone.

Google and Tor

![](image_rsrcYK.jpg)

What does Google think of Tor? Quite honestly, I suspect they try not to. In all probability, they probably don't hate it like the NSA does, but they know that if every Google user used Tor on a daily basis, much of their ad targeting system would begin firing blanks. Imagine if a thirteen year old boy received ads for Cialis, or an eighty-year old woman named Bertha began to see ads for Trojan coupons. It makes for a lousy targeting system. That's good for us. Not so much for Google.

They don't mind donating funds, either, since this allows a future stake in the technology. To that, they've not only donated to Tor, but to other anonymity services too, like Freenet. They've even donated to Mars rover technology. All kinds of outer space things. They never know which technology is going to rocket into orbit a week or year from now, so they throw money around like Scrooge on Christmas morning.

Captchas

At times you'll be using Tor and find that Google spits this requirement out in order to prove you're human. This, on account of their massive analyses on search queries, is what drives some Tor users to think Google has it out for them.

However, Google has to put up with lots of spammers and general thievery; bots hammering the servers with tons of queries in short amounts of time that, when added up, puts a huge strain on the servers. It can be just one thing, but it can also happen if your employer uses proxies. For instance, many employees working for the same company that uses one of these can set off a red flag. When your Tor circuit switches to a new one, though, usually it solves itself. There are other search engines like DuckDuckGo you can use, however, if Google is giving you headaches.

SpiderOak

Normally I warn against using Cloud Service for anything you want private. SpiderOak is one exception I can vouch for, with some reservations. It's a decent enough alternative to DropBox as it's coded with "Zero Knowledge" (so say the developer) and when you install it, a set of encryption keys is created, client-side. When you upload data to SpiderOak servers, they're encrypted on *your* computer and *then* uploaded.  Again, according to the developers.

They claim that even if a subpoena requires subscriber data, they could not deliver it since only you have the keys. That sounds very secure, but I still wouldn't upload anything unencrypted that might pique Edward Snowden's curiosity. If it pique's his mind, it'll pique other, more powerful types. Encrypted container files fall into this category.

The other downside is that it's centralized. Centralization means a single-point-of-failure. As well, your data can be deleted by them at any time (true with any online service really). Remember that between you and a judge, they will always side with the judge.

Tails

Ever heard of a "live system"? Neither had I until Tails burst on the scene in 2009\. Tails allows you to use Tor to avoid tracking and censorship, and in just about any location you could want. It houses its own operating system, the best part being that it's designed for those on the go.

You can run it via USB stick, SD or even a DVD. This comes pretty handy as it makes it resistant to viruses. It's also beneficial if you don't want your hard drive to leave remnants of your browsing session. The best part is that it's free. Most things based on Linux are, but Tails comes with chat client, email, office, and browser.

The downside to using a DVD though, is that you must burn it again each time you update Tails. That's the inconvenient part. So let's install it to USB stick instead.

1.) Download the Tails installer from the [Tails website](https://tails.boum.org/install/). You must first install it somewhere, like a DVD, and THEN clone it the USB stick or SD card.

2.) Click Applications --> Tails --> and then on 'Tails Install' to begin the installation.

3.) Choose Clone & Install to install to SD card or USB Memory Stick

4.) Plug in your device, then scan for the device in the Target-Device drop down menu. You'll get a warning about it overwriting anything on the device. That's nothing to worry about, so choose yes and confirm the install.

Tails Limitations

Neither Tails nor Tor encrypt your documents automatically. You must use [GnuPG](https://www.gnupg.org/) or LUKS for that, bearing in mind that some documents like Word or Atlantis may have your registration info within the document itself. This can be a problem for anonymity. Case in point: in 2013, Amazon self-publishers discovered that pen names could sometimes be revealed by looking at the code of certain word documents and siphoning out the registration information. This code revealed the real identity and addresses of many self-published authors. As an author myself, trust me when I say you don't want the headaches that come with that.

Personally I enter in fake information whenever I "register" any app. All the more so if I will use that app in conjunction with Tor or Tails.

There's other noteworthy stuff to know if you're aim is true anonymity.

Namely:

- Document metadata is not wiped with Tails.

- Tails doesn't hide the fact that you're using it from your ISP (unless you use Tor bridges). They cannot see what you're doing on Tor, true enough, but they know you're using it. Again, unless you use a Tor Bridge.

- Tails is also blind to human error. Try not to use the same Tails session to begin two different projects. Use separate sessions. Isolating both identities in this way contributes to strong anonymity for your sessions.

Chrome

Using Tor with Firefox is hardly the only way to slay a dragon. There's also Chrome. Yes, it's Google, and yes, Google has strayed far from it's "Do No Evil" motto, but like everything else in life, luck favors the prepared and you'd be surprised at how much you can lock down your browser from invaders. Preparations are everything. You just have to have the right sword. The right armor. The right lockpicks. The preparations (reagents) are as follows:

I. Install the [ScriptNo](http://code.google.com/p/scriptno/) extension. It is to chrome what a mouse is for a PC, at least as far as precision goes. It offers excellent control, even allowing you to fine-tune the browser in ways that NoScript for Firefox cannot. If you find it too difficult, [ScriptSafe](https://chrome.google.com/webstore/detail/scriptsafe/oiigbmnaadbkfbmpbfijlflahbdbdgdf?hl=en) is another option. I've used both and came away very satisfied, though like everything else on the internet, your mileage may vary.

II. [Adblock](https://chrome.google.com/webstore/detail/adblock/gighmmpiobklfepjocnamgkkbiglidom?hl=en). This one is just insanely good at repelling all kinds of malware. It's probably the most well-known too, so there's plenty of feedback scattered across the internet.

III. [User-agent Switcher](https://chrome.google.com/webstore/detail/user-agent-switcher-for-c/djflhoibgkdhkhhcedjiklpkjnoahfmg) for Chrome. Install it. It mimics user-agent strings. You can set yours to look like Internet Explorer and this will fool a lot of malware payloads into thinking you're really browsing with Internet Explorer and not Firefox or Chrome, thus firing blanks at you.

V. [CanvasBlocker](https://addons.mozilla.org/en-US/firefox/addon/canvasblocker/) - This prevents sites from using Javascript <canvas> API to fingerprint users.  You can block it on every site or be discriminant and block only a few sites. It's up to you. The biggest thing for me is that it doesn't break websites.

Deadly Firefox Options

Firefox

You might be tempted to enable "Check for counterfeit websites" in Firefox. Don't do this, as it will relay sites you regularly visit to Google's servers. Google's "predictive text-search" is also bad as it relays keystrokes to Google as well. To change it you have to do it manually by going into about:config in the Firefox address bar. 

Now let's look at some other privacy settings you might want to know about.

Javascript - This one you should avoid like the black plague, as using it on the Tor network is equivalent to drinking from a well contaminated by the plague in the year 1350\. You may notice it is turned on by default under the Firefox options tab, though. The reason is spelled out by the Tor Developer Team:

We configure NoScript to allow JavaScript by default in Tor Browser because many websites will not work with JavaScript disabled. Most users would give up on Tor entirely if a website they want to use requires JavaScript, because they would not know how to allow a website to use JavaScript (or that enabling JavaScript might make a website work).

There's a tradeoff here. On the one hand, we should leave JavaScript enabled by default so websites work the way users expect. On the other hand, we should disable JavaScript by default to better protect against browser vulnerabilities ( not just a theoretical concern!). But there's a third issue: websites can easily determine whether you have allowed JavaScript for them, and if you disable JavaScript by default but then allow a few websites to run scripts (the way most people use NoScript), then your choice of whitelisted websites acts as a sort of cookie that makes you recognizable (and distinguishable), thus harming your anonymity.

Ghostery and Ghostrank - These aren't particularly deadly, just useless on Tor since Tor disables tracking anyway. If you do decide to use it, know that using either can alter your browser 'fingerprint' - though not to the extent of breaking anonymity. Ghostery still blocks any tracking scripts regardless if you're on Tor or not. But use DuckDuckGo if you want to beef up your anonymity.

Adblock - We mentioned this one before and, sadly, using this could also change your browser fingerprint. Adblock plus has "acceptable ads" enabled by default, and there is also the [scandals](http://www.wilderssecurity.com/threads/german-blogger-calls-adblock-plus-a-mafia-like-advertising-network.349411/page-8#post-2319328) that Adblock has been in over the years, one implying that Google paid the Adblock CEO for Google Ads to be shown. You can draw your own conclusions about that, but with so many users applying pressure, you can rest assured that you're not just a number to them anymore.

Besides that, the basic idea of the Tor Browser Bundle is to use as few addons as possible. They figure that TorButton, NoScript, and HTTPS Everywhere is sufficient to preserve anonymity without the added risk of additional addons. Or drama. Along this line of thought, the [Panopticlick website](https://panopticlick.eff.org/index.php) may also be useful to you.

Whonix & Tor

If you're paranoid that using Tor could get you into trouble, such as if you host a Hidden Service, you may want to look into [Whonix](https://www.whonix.org/wiki/Main_Page) before running anything further. Many power users who use Tor on a daily basis like the tighter security it offers. Both tools offer their own strengths and weaknesses, and each strength is meant for a different purpose. You may find one is better than the other for your personal situation, where the situation differs according to your security needs.

Like Tails, Whonix is built with anonymity and security in mind. It's also based off of Debian/Linux, so it's a good synergy where anonymity is concerned. This synergy grants anonymity by routing everything through Tor. The advantages are that DNS leaks are next to impossible and malware cannot reveal your IP address. In fact, the only connections possible are routed through Tor via the Whonix-Gateway.

![](image_rsrcYM.jpg)

The question you may be wondering is: how much security is too much security? What's overkill and what isn't?

Well, the perfect answer to that is this: How far will you fall if caught, and how much time are you willing to invest in reading to prevent it? Tails is easier to grasp, and if you don't expect attacks from sites you visit, then by all means use Tails.

If, however, you live in North Korea or China, then there's the possibility of twenty years of hard labor - hammering worthless rocks. That is, if they see any Tor activity coming from your location that correlates to "things they don't like" activity... or anything else in the case of North Korea. They don't like it when outsiders offer the peasants hope. If you're caught in that country, you'll be found guilty long before you ever see a judge.

A few notable features of Whonix that make it more secure:

Anonymous Publishing/Anti-Censorship

Anonymous E-Mail w/Thunderbird or [TorBirdy](https://addons.mozilla.org/en-us/thunderbird/addon/torbirdy/)

Add proxy behind Tor (user -> Tor -> proxy)

Chat anonymously.

IP/DNS protocol leak protection.

Hide that you are using Tor

Hide the fact you are using Whonix

Mixmaster over Tor

Secure And Distributed Time Synchronization Mechanism

Security by Isolation

Send E-mail anonymously without registration

Torify any app

Torify Windows

Virtual Machine Images (VM)

VPN Support

Use Adobe Flash anonymously

Use Java/Javascript anonymously

The following is an example of a moderately secure system:

- Host Whonix on a memory stick with a flavor of Linux of your choice

- Use a VPN you trust.

Two other things to note where security is concerned:

- Avoid regular calls of non-Tor WiFi tablets if you're using Cafe WiFi

- Know as well where every CCTV is located in the area you plan to use Tor

MAC Addresses

A new WiFi/Ethernet card has something that can aid in tracking you. It's a 48-bit identifier burned-in by the manufacturer. Sort of like an IMEI for your phone. If by chance you weren't thinking clearly and bought your computer with Tor in mind using a credit card, you may later get targeted by an FBI "NIT" that swipes your MAC number. A Nit is short for 'Network Investigative Technique'. If that happens, you're toast, as you'll be tracked by some lackey working for them with far too much time on his hands.

The way to defeat this is to have a disposable MAC address (the number, not the Apple product) - one that you bought with cash with no security cams looking over your shoulder. That way you can get rid of it in a flash or swap it out if you realize they're onto you.

Whonix Bridges

Using a Bridge with Whonix can be beneficial.

What Bridges Are

Bridges are obfuscation tools used to cloak your Tor usage from a nosy ISP or government who might see you're using Tor, but not know what you are doing with it. To that end, Tor bridges are alternative ways to enter the Tor network. Some are private. Many are public. Some are listed on the Tor homepage. In a hostile environment, you can see the value in using it to your advantage as it makes it much more difficult for an ISP to know you're using Tor.

What Bridges Are Not

While not especially unreliable, they are certainly *less* reliable than regular Tor usage where performance goes. But the tradeoff may be in your best interest. Only you can decide if the performance hit is warranted. Here's how to do it in Whonix.

Bridges must be added manually since there is no auto-install method for Whonix, but it's not that difficult. You simply must enter them into the proper directory, like so:

/etc/tor/torrc.

If you're using a graphical Whonix-Gateway, then you need to browse to:

Start Menu -> Applications -> Settings -> /etc/tor/torrc.examples

To edit your torrc file (which is necessary for bridge adding), browse to:

Start Menu -> Applications -> Settings -> /etc/tor/torrc

Then add whatever bridge you copied from the Tor bridges page (or a private one if you have it). Then restart Tor for it to take effect.

Using Your Real Name Online Outside of Tor

What kind of danger is there in using your real name online?

I hate to say it but even with all I've learned the answer is still the same now as it was way back when Facebook first hit the scene. In fact, I suspect it's the same now as it was in my early teens when I crept around an online watering hole called The Well.

The answer is this: It depends.

Law enforcement and prospective employers who mine your social media profiles for data are often worse than thieves who salivate when you announce on Twitter you'll be out of town for two weeks. Thieves, while unsavory to be sure, are more honest in their profession than a lot of the corporate behemoths that do things behind your back.

Employers are the worst of the lot. As hypocritical as Harvey Two-Face. They demand transparency in your life but never their own. Make an inflamed political post or drink wine on vacation in Bora Bora with half-naked Filipinas as those fire-twirlers do their thing in the background, and you could lose your job... or even be denied one. Not kidding. It happens. Likewise, if you mention on your resume that you use Tor, you may one day hear your interviewer ask:

"I noticed you're a big fan of Tor and other anonymity tools that shield your IP address and prevent better relationships between consumers and companies... Could you elaborate on why you need to use an anonymizing service? We like transparency in our employees."

Yes, I was actually asked this in an interview for a position that handled a lot of money. But as soon as she said 'consumer', I knew what she really thought of me. Consumer is a word meant for the animal kingdom. Squirrels, for instance. Raccoons and other rugrats. Beasts that roam on all fours and are slaves to instinct. Beasts that don't pray, forgive or sing praises to a Higher Being they can neither feel, see, nor hear.

I'm thankful for the upfront honesty, actually, but what really bothered me was the casual way it was asked, like every applicant should have something to hide if they like anonymous communications. Like some wet-behind-the-ears greased up code monkey in the hacker clan Anonymous and up to no good. At any rate, she didn't like my answer.

"Because I value freedom."

That sunk my battleship. I came out of that interview perplexed, yet jobless, viewing privacy as somewhat of a double-edged sword since one needs an online presence for many higher paying employers. It didn't sit well with me in the long run. I felt a little cheated to be honest, and as I drove home some of the mumblings I'd overheard later on became as loud as roaring trains in my ears. Here's a few tidbits:

- Don't like someone on Facebook? You probably won't like working with them.

- Like the competitor's products? Here's our three-year non-compete agreement for you to sign.

- You use Tor? The only people that use that are terrorists, pedos and hitmen. You must be one of those buggers.

Soon thereafter, any time a prospective employer noticed "Tor" under the Hobbies section of my resume, it would always illicit a negative response. Like witchcraft or Dungeons and Dragons Dungeonmaster. My breathing seemed to become erratic as my heart raced, as if they were about to summon an unbadged "authority" to warn me of being too private.

He'd be dressed like Dilbert, only skinnier and with a bumblebee-yellow pen and a clipboard. He'd have multiple facial tics and that annoying eyebrow raise, as if it were completely illogical to value privacy. I have no idea why he'd have a clipboard, but he always did in my minds eye.

My solution was to divide my public and private identity in social settings and remove any trace of it on my resume. In fact, I refused to give any indication on any social media site, either, that I was into any of the following:

- PGP

- Encryption, or encrypting files or Operating Systems

- Tor Relays

- I2P

- Freenet

- Anonymity in general

- Anything linked to Edward Snowden

Such is the nature of the masses. One simply cannot rely on Facebook or Twitter or Google to respect one's freedom to use Tor without announcing it to the whole world. But at least with Tor, Google cannot mine your browsing session for ads. No ads = no soup for them. From NBC:

"The Internet search giant is changing its terms of service starting Nov. 11\. Your reviews of restaurants, shops and products, as well as songs and other content bought on the Google Play store could show up in ads that are displayed to your friends, connections and the broader public when they search on Google. The company calls that feature "shared endorsements.''

So I firewall everything I do. I use [Ghostery](https://www.ghostery.com/) for social sites and offer only pseudonymous details about myself. In fact, I try to avoid any correlation between Tor and any social media site just as one would a can of gasoline and a lighted match.

Email Anonymity

Is it possible to send a message that is foolproof against trackers, hackers and Big Companies?

There are, in fact, many flavors to choose from to accomplish this task. Below are a few rock-solid services. Combined with Tor, they grant you a virtual fortress.

[W3, The Anonymous Remailer](http://gilc.org/speech/anonymous/remailer.html)

![](image_rsrcYN.jpg)

Connectable with Tor, you only need an email address to send the message to (preferably encrypted with PGP--more on that in a moment).

Another is [Guerrilla Mail](https://www.guerrillamail.com/). They allow users to create throwaway emails to be used at leisure. Emails sent are immediately wiped from the system after you hit Send. 

![](image_rsrcYP.jpg)

These services claims of anonymity would be pretty thin if we did not encrypt our messages-- which brings us to PGP.

[PGP](https://en.wikipedia.org/wiki/Pretty_Good_Privacy) is the encryption standard of choice for many old users like myself, and for good reason. It has never been cracked by the NSA or FBI or any intelligence agency and likely won't until quantum computers become common. It works by way of key pairs, one which is public and one private (the one you will use to decrypt your messages with).

Worry not about the term "keys". It is not difficult to grasp and will be as easy as hitting send once you've done it a few times.

The first thing you must do is make your public key available. This is only used to verify your identity and is not the same as divulging your passphrase for say, a Drivecrypt container. Your recipient must also share with you their key so you can respond in turn.

Only the two of you will be able to read each other's messages. The caveat is if the other person is compromised and you don't know about it. They will read everything you encrypt. Here is what you need to know:

1.)  To begin, make two keys, one public--for everyone else but you--and one that you wouldn't even share with your own mother. You should back this key up in a secure medium, and remember that if it isn't backed up to three different types of media, it isn't backed up. If your truly paranoid, send one on an encrypted microSD to your parents in case of housefire. Yes, it does happen.

2.) If however you opt to tell mom, then she will need your public key (you did publish it on a public key server, right?) Then you can read it by way of your private key. She doesn't know this key (thank the gods!)

3.) You can "sign" any message you want over Tor or anywhere else (Freenet, for example, the highest security setting of which demands absolute trust of your friend's darknet connection) to verify it is really you sending it.

...Unless Norman Bates does a shower scene on you and takes your keys. Your mom can then verify with your public key that it is really you.

4.) Users you've messaged with (or not) can sign your public key as a way of verifying your identity. As you can see, the more people that do this, that is, vouch for you, the better.

Important:

Unless you've got the photographic memory of Dustin Hoffman in Rainman, it's a good idea to store your public/private keys and passwords and also revocation-certificate to backup media so you can retrieve it five years down the line... should you need it. And believe me, you will!

Encrypt them in containers. Always print your key-file or pass phrase and deposit in a safe place. If you lose it, all documents encrypted with it are permanently lost. There are no back-doors and no way to decrypt without it. Also, consider making an expiration date at key-pair creation.

If you like nice and easy interfaces, try [Mymail-Crypt](https://chrome.google.com/webstore/detail/mymail-crypt-for-gmail/jcaobjhdnlpmopmjhijplpjhlplfkhba) for Gmail. It is a plugin that allows users to use PGP-encrypted messages in a handy interface, though ensure your browser is air-tight secure and you trust it with your private key.

With that said, let's configure PGP for Windows

- Install [Gpg4Win](http://gpg4win.org/download.html)

- Next, create your key in [Kleopatra](https://www.kde.org/applications/utilities/kleopatra/) and choose Export-Certificate-to-Server by right click so you can publish it to a keyserver. Get a trusted friend to "sign" and establish trust.

- Use Claws-Mail client that comes packaged with it or use [Enigmail](https://www.enigmail.net/download/) if you're using Thunderbird.

- Send a few messages back and forth to your trusted friend via PGP to get the hang of things.

- Optionally you can set a Yahoo/Gmail/Hotmail filter so as to forward any messages that contain "Begin PGP message" to a more private account.

[Freenet](https://freenetproject.org/download.html)

This is the granddaddy of all anonymous systems the world over, both for file sharing or any kind of secret chats. But it is also headache inducing because it is not especially beginner friendly. Explaining everything it has to offer goes far beyond our Tor discussion as they are two different systems, but I include it here as an alternative if you find Tor lacking.

And it is not as simple as Tor, nor is it as fast unless you leave it running 24/7\. It is not for everyone as there are all manner of criminal entities that use it and you will notice this if you load up any groups. It is hard to ignore and unlike Usenet, there is no one to file a complaint with. No one to report. It is anarchy multiplied many times over in many groups, but there are ways of mitigating the damage.

But for absolute anonymity and freedom of speech, there is no better tool to use if you have the patience to learn its darknet offerings.

From the website:

Freenet is free software which lets you anonymously share files, browse and publish "freesites" (web sites accessible only through Freenet) and chat on forums, without fear of censorship. Freenet is decentralised to make it less vulnerable to attack, and if used in "darknet" mode, where users only connect to their friends, is very difficult to detect.

Communications by Freenet nodes are encrypted and are routed through other nodes to make it extremely difficult to determine who is requesting the information and what its content is.

Users contribute to the network by giving bandwidth and a portion of their hard drive (called the "data store") for storing files. Files are automatically kept or deleted depending on how popular they are, with the least popular being discarded to make way for newer or more popular content. Files are encrypted, so generally the user cannot easily discover what is in his datastore, and hopefully can't be held accountable for it. Chat forums, websites, and search functionality, are all built on top of this distributed data store.

An important recent development, which very few other networks have, is the "darknet": By only connecting to people they trust, users can greatly reduce their vulnerability, and yet still connect to a global network through their friends' friends' friends and so on. This enables people to use Freenet even in places where Freenet may be illegal, makes it very difficult for governments to block it, and does not rely on tunneling to the "free world".

It is not as simple as using a Usenet provider's newsgroup reader. No sir, Freenet requires patience. Using Frost or Fuqid (Front End apps for the main Freenet program), it might be half an hour before you can "subscribe" to groups or download in the way you can Usenet. Some groups, like the Freenet group and other technical groups will be immediately available, but with few messages. Time will solve this. So keep it running in the closet and forget about it for a day or so if you plan on subscribing to a lot of groups.

It will be worth the wait.

Frost & Fuqid

The two free front ends I recommend are: Frost and Fuqid.

Frost has seen a lot of improvements but I recommend you try Fuqid first as it is the first external app for Freenet that acts as as an insert/download manager for files. Fuqid stands for: Freenet Utility for Queued Inserts and Downloads and runs on Windows or Linux under wine.

The Fuqid freesite is on Freenet itself at:

USK@LESBxzEDERhGWQHl1t1av7CvZY9SZKGbCnsD7txqX0I,nP0CHuKvlbVzcrnz79TEd22E56IbKj-KHB-W8HHi9dM,AQACAAE/Fuqid/-1/

You will need to paste the above into Freenet's front control panel where it says "Key". It can take several minutes to load if you're new to the system.

After you've installed it, right click on the left side with your list of boards and choose "Add new board". For the name put in "fuqid-announce" with out the quotes. You will now find a new board called "fuqid-announce" in your list of boards.

Right click this board and choose "Configure selected board". This will bring up a new window. On that window click "Secure board" to change it from a public board. Now in the section that says "Public key" paste in the key below:

SSK@qoY-E5SKRu66pmKH64xa~R~w3hXmS5ZNtqnpEGoCVww,HTVcdWChaaebfRAublHSxBSRaRFG91qCwsa3mGF3-QE,AQACAAE

Passwords

Good, strong passwords are like having a couple of Rottweilers sleeping in your den. Most intruders will leave when the chaos starts. Weak passwords are like having a Golden Retriever. Nice and friendly and easy to trust around kids, but might just let out a little woof at 3AM when said intruder comes. Then he will hide under the coffee table (the dog, not the intruder).

I've heard for years that you should never use anything personal as your password. That includes family names. Favorite books. Movies. So what's the solution?

Remix your passwords with a symbol or two. If you think a hacker won't be able to guess the name of your girlfriend's locker combination, you'd be mistaken. It is dirt simple to guess even if you mix it up a bit. Computers devoted to this practice can guess many in less than a nanosecond.

But how do you remember a password for a site used over Tor that has symbols?

- Easy. Use a passphrase that is simple to recall for you only. First write out the first letter of each word, taking not of case and position. Insert symbols therein. For instance:

Last Sunday, the wife bought me a Rolex watch and it was too ugly.

Which when changed is:

LS,twbmarwaiw2u

The above pass is hard for a hacker to guess but easy for you to remember... assuming you are good at substitution.

Changing Your Passwords

Provided you've followed the above to the letter, you shouldn't have to rotate out your passwords every 90 days. I'm sure you've heard from both sides of the aisle their say on the subject, but I believe research has proven that keeping a strong password (unless proof of compromise) is a safe bet.

The research paper from ACM/CCS 2010: "The Security of Modern Password Expiration: An Algorithmic Framework and Empirical Analysis" by Yinqian Zhang, Fabian Monrose and Michael Reiter came to the conclusion that changing passwords every few months did not, repeat, did NOT increase security:

at least 41% of passwords can be broken ofﬂine from previous passwords for the same accounts in a matter of seconds, and ﬁve online password guesses in expectation sufﬁces to break 17% of accounts.

....our evidence suggests it may be appropriate to do away with password expiration altogether, perhaps as a concession while requiring users to invest the effort to select a signiﬁcantly stronger password than they would otherwise (e.g., a much longer passphrase). ....

In the longer term, we believe our study supports the conclusion that simple password-based authentication should be abandoned outright.

Storing Passwords in Tor Browser

You may have noticed that the "Remember Password" option in Tor Browser is not available, or so it seems. But if you look at the privacy setting and alter the history setting to "remember history" and "remember passwords for sites," it will no longer be greyed out.

Diceware

If you must store passwords, a good option for a unique random one is [Diceware](http://world.std.com/~reinhold/diceware.html) – where you can get an expire date for any password months from the date of creation. You can copy any password to a text file then encrypt it and mail it to yourself or place on a removable (encrypted) drive or USB stick.

Remember: Tor does nothing to improve the security of your *system* to everyday attacks. It only improves security online, and even then only when used responsibly. Tor has no idea if your version of Windows is unpatched and infected with a zero-day malware payload that infected it with a keylogger.

One way in which a hacker could guess your complex password is if they linked your Tor usage with non-Tor usage and compromised your passwords from a non-Tor site. This is why you should never use the same usernames/passwords for Tor that you do for non-Tor activity.

Preventing Non-Tor Activity From Being Linked with Tor Activity

It is risky to browse different websites simultaneously and preserve anonymity since Tor might end up sending requests for each site over the same circuit, and the exit node may see the correlation.

It is better to browse one site at a time and thereafter, choose "New Identity" from the Tor button. Any previous circuits are not used for the new session.

Further, if you want to isolate two different apps (allow actions executed by one app to be isolated from actions of another), you can allow them to use the same SOCKS port but change the user/pass.

Keyloggers

You might wonder what a keylogger has to do with Tor. Or for that matter, what a keylogger even is. You're not alone. In fact you'd be surprised how many people don't know and shocked how many techs consider them a non-issue.

In 2010 I caught up with an old childhood friend of mine I had not seen in over a decade. He was now an ATF agent. I was surprised and (falsely) assumed his extensive training meant he knew as much as an NSA agent when it came to computer security. Wrongo.

He replied to a post I made on a Facebook regarding the hacking group "Anonymous."

"What's a keylogger?" he asked. I waited for someone else to reply. No one did so I told him. He seemed amazed, dumbfounded, as though it were something only recently unleashed upon the net. I then told him that they had been around a long time.

But (sigh), there's a lot of confusion on what they do exactly. Some people call them spyware. Others say they're trojans. Still others, exploits. They're a little bit of everything to be honest.

They are surveillance software that tracks and records every click you make, every website visited, every keystroke typed. Chats, Skype, Emails. If you can type it, it can record it and all right under your very nose. It can even email what you type to a recipient on the other side of the world. CC numbers, passwords and Paypal login details are just the short list of targets it can acquire.

So how does one get in infected?

- Opening an email attachment

- Running an .exe file from a P2P network from an untrusted user

- Accessing an infected website with an outdated browser

- The NSA, if they can grease the right palms

Some employers use them to track productivity of employees. Some wives attach one via USB (Hardware version) to see who their hubbies are conversing with at night after bed. Parents use them on the kid's computer. So it isn't like they're 100% malicious all the time.

But they are devilishly difficult to detect. They wield an almost vampiric presence, but like vampires there are subtle signs you can glean without whipping out a wooden stake.

Signs

- Sluggish browsing speed

- Laggy mouse/pausing keystrokes in a text doc

- Letters don't match on display with what you type

- Errors on multiple webpages when loading heavy text/graphics

There are two types:

Software Keyloggers

This type hides inside your operating system. They lurrrve Windows. Linux, not so much. The keylogger records keystrokes and sends them to a hacker or other mischief maker at set times provided the computer is online. Cloaked, most users will never see it working its dark art. Many popular anti-virus vendors have trouble identifying it because the definitions change so frequently.

Hardware Keyloggers

Bond might have used one of these. Being hardware, it is a physical extension that can plug into any USB on a PC and can be bought online by suspecting spouses or kids wanting access to their dad's porn stash. Keystrokes are logged to ram memory. No install needed.

Thus, unless you're the type to check your PC innards every day, you might not spot it until it's too late. They also can be built right into the keyboard. The FBI loves swapping the target's out with a carbon copy custom-built surveillance device. Granted, this is mainly for high-value targets like the Mafia but they're available to anyone.

Keylogger Prevention

- Check your keyboard for suspicious attachments. If you are an employee at X company and a new keyboard arrives at your desk one morning, exercise caution unless you trust your boss 200%.

- Use a Virtual Keyboard. No keystrokes = no logging!

- Use [Guarded ID](http://www.guardedid.com/) to prevent hackers from capturing your keystrokes. It works by scrambling everything you type, rendering any info useless to hackers.

- Use a decent firewall to stop a keylogger from delivering your data. A year ago, my Comodo firewall alerted me to suspicious network activity seemingly out of nowhere when I wasn't doing anything online. Turns out I had the Win64/Alureon trojan. I had to use Malwarebytes to detect and remove it. Norton was useless! Imagine that.

Other Anti-Keyloggers

If you do not mind spending some coin, there are a few more:

Zemana AntiLogger (Free)

![](image_rsrcYR.jpg)

This "free" version is a bare-bones keylogger-detector. In fact, it's quite stripped down but if all you require is being alerted then this might be for you. The Keylog Guard offers encryption for all things typed at the keyboard. Any snooper will only get garbled letters from you. The paid version is somewhat pricey at $29.99 and comes with extra-protection for malware and such but is a bit overkill.

Also, it will nag you if you try and run something safe it doesn't like, much like every other anti-virus will.

SpyShelter STOP-LOGGER

![](image_rsrcYS.jpg)

The Free version offers more than Zemana does in that you get screenshot capture. It will also alert you to any code that tries to swipe your keystrokes from you but the Free version is not 64-bit compatible.  It is $24.99.

Be aware, however, that removing a keylogger is nasty business as they have a habit of reinstalling themselves. Keyloggers will often hide as a service in svchost.exe so task manager isn't much help without a dedicated app. The optimal way of prevention is to stop them in their tracks before insertion.

Be proactive. Anticipate a password compromise. Remember, vigilance!

Darknet Markets

Some of you might be wondering how safe a Darknet really is in light of the vulnerabilities discussed. The short answer is this: As safe as you make it. 

You are the weak link. The last link in the security chain. And although you need Tor to access Onion sites, the term can apply to any anonymous network - networks like I2P or Freenet or anything else that cloaks the source of data transmit, and by extension, your identity.

Which brings us to the Darknet Marketplace.

The complete list of such marketplaces on the deep web are numerous, and the risk of getting scammed is quite high. It's one reason why you may not have heard about them. They are often taken down quickly by either a venomous reputation or a law enforcement bust. Sometimes they piss off the wrong people and then spammers ddos the site. But there are numerous places one can go if you're curious about what is sold by whom.

When I say sold, what I mean is... Anything you want that cannot be gained through the usual legal channels. And remember that what is legal in one country may be illegal in another. In Canada, lolicon comics are illegal and can get you in big trouble if you cross the border. But not in America. In the USA you can pretty much write any story you want. In Canada? TEXT stories involving minors are verboten.

The other difference is that there are safety nets in buying almost anything in a first world country on the open market. Think BestBuy. Mom and Pop stores. Florist shops. If customers get injured, what happens? Customers sue via the legal safety net and make a lot of lawyers a lot of money.

But the Darknet Marketplace laughs at any such safety nets. In fact, you're likely to get scammed at least a few times before finding a reputable dealer for whatever goods you seek. And it really doesn't matter what it is, either - Teleportation devices? Pets? Exotic trees? It's all the same that goes around. Whatever is in demand will attract unsavory types and not just on the buyer's end.

Therefore, research any darknet market with Tor, being careful to visit forums and check updated information to see if any sites have been flagged as suspicious or compromised. Some other advice:

- Always use PGP to communicate.

- Never store crypto-currency at any such marketplace.

- Assume a den of thieves unless proven otherwise by *them*. The responsibility is theirs just as it is offline, to prove they are an honest business. If you open your own, keep this in mind: customers owe you nothing. You can only betray them once.

So then, how does one tell a scam?

Because many new darknet vendors will arise out of thin air, with rare products that will make customers swoon and send them money... without doing any research on their name or previous sales. A real hit and run operation. Hit quick and fast and dirty. Seduce as many as they can before the herd catches on to the wolf in disguise. Many are suckered, thinking "it's only a little money" but a little money from a lot of Tor users goes a long way in encouraging other scammers to set up shop.

When you ask them why they do not offer escrow, they say "We think it is unreliable/suspicious/unstable" amid other BS excuses. It is better to hold on to your small change than leave a trail to your treasure chest. And make no mistake some of these scammers are like bloodhounds where identity theft is concerned.

- Do your research. Check forums and especially the dates of reviews they have. Do you notice patterns? Are good reviews scattered over a long period of time or is it rather all of a sudden--the way some Amazon affiliate marketers do with paid reviews that glow? Not many reviews from said customers?

If you've seen the movie "Heat," with Al Pacino and Robert de Niro, you know when it is time to Walk Away. In the middle of a nighttime heist, Niro goes outside for a smoke. He hears a distant cough. Now, this is middle of the night in an unpopulated part of the city that comes from across the street - a parking lot full of what he thought was empty trailers. Hmm, he thinks. Not so empty (it was a cop). He walks back into the bank and aborts.

The other aspect is time. Some fake sites will set a short ship time and count on you not bothering to see the sale as finalized before you can whistle Dixie out of your ass. After finalization, you're screwed since the money is in their wallet before you can even mount a protest.

Fraud Prevention

One is Google, believe it or not, at [http://www.google.com/imghp](http://www.google.com/imghp). Dating sites like Cherry Blossoms and Cupid sometimes use reverse image search to catch fakers and Nigerian scammers masquerading as poor lonely singles to deprive men of their coinage. If they can catch them, so can you. If the image belongs to some other legit site, chances are it is fake. [Foto Forensics](http://fotoforensics.com) also does the same, and reports metadata so that it becomes even harder to get away with Photoshop trickery.

When it is Okay to FE (Finalize Early)

FE means 'Finalize Early'. It's use online can usually be found in black marketplaces like Silk Road and Sheep's Marketplace. It simply means that money in escrow is released before you receive your product. Every customer I've ever spoken with advises against this unless you've had great experience with that business.

Buuut... Quite a few vendors are now making it a standard practice to pay funds up front before you have anything in your hands.

On more than one Marketplace forum, there's been heated exchange as to when this is proper. You might hear, "Is this guy legit? What about this Chinese outfit over here? He seems shady," and others: "A friend said this guy is okay but then I got ripped off!". You get the idea.

Here is my experience on the matter.

1.) It is okay when you are content with not getting what you paid for. This may seem counterproductive, but think how many gamblers go into a Las Vegas casino and never ask themselves "How much can I afford to lose?"

The answer, sadly, is not many. Vegas was not built on the backs of losers. Some merchants do not like escrow at all. Some do. So don't spend more than you can afford to lose. Look at it the way a gambler looks at making money.

2.) It is okay when you are guaranteed shipment. There are FE scammers out there that will give you an angelic smile and lie right into your eyes as they swindle you. Do not depend solely on reviews. A guy on SR can be the best merchant this side of Tatooine and yet you will wake up one day and find yourself robbed. He's split with a million in BTC and you're left not even holding a bag. Most won't do this to you. But a few will.

When it is NOT Okay to FE

- When losing your funds will result in you being evicted or a relationship severed. Never borrow money from friends and especially not family unless you want said family to come after you with a double-bladed ax. If you get ripped off, you lose not only the cash but the respect and trustworthiness of your family. Word spreads. You don't pay your debts.

Darknet OPSEC

"Three can keep a secret if two of them are dead..."

- Ben Franklin

The above quote was a favorite of mine in elementary school. It was applicable then just as it is now to having a secure mindset, and boy how I loved spouting that line whenever a friend begged me to confirm a rumor he'd heard. A rumor that, if validated, could have landed me in hot water with my red-headed chem teacher. Luckily I knew when to keep my mouth shut.

As you should.

Keeping your mouth shut about Darknet markets is more important than any encryption scheme you use, passphrase you know, Freenet group key or anything related to your Bitcoin wallet. Knowledge is power.

No, strike that. Knowledge is potential power. And power in slippery hands can be disastrous. Playing the bar braggart might be fun after a few beers and win you a few points with other guys, but it gets more people imprisoned over frivolous reasons than anything else I can think of. And I've seen more than one friend go down in flames because they mentioned a darknet market to someone they thought they could trust. But then that friend told someone else he trusted, more than anyone in the world. We''ll call my friend Grady.

Grady told his girlfriend. Spared no details of his darknet ops and how they traversed several continents. He made himself sound like Agent Smith from the Matrix. I shook my head upon hearing this...

Cue Fred Sanford: "You Big Dummy!"

Trusting her to keep his secret was not just dumb, it was galactically stupid. Like expecting Eve to eat the forbidden fruit all by herself. And we know how that story ends. Misery truly loves company.

Next thing he knew, he attracted the attention of the authorities in Hong Kong, one of which was her father. The secret was safe enough he supposed, until he refused to marry his hyper-critical girlfriend, claiming he had taken the "Red Pill" and feared settling down with an ultra-hardline feminist harpy (his words) would kill his dreams. Well it killed something alright. His freedom.

Lesson? You can't fix stupid, so why would you trust it?

While you needn't go totally dark about your darknet knowledge for all eternity, in real life conversations, Social Media outlets, Tinder, Skype, etc., mums the word. Invoke radio silence where applicable or better yet, feign ignorance. If they show you proof, simply say you have good connections. Then buy them a beer and leave. If they still persist, consider warning them you're about to sever all connections to them. Friends come and go, but freedom is priceless.

Running a Hidden Tor Server

Having used Tor for many years, it came as a pleasant surprise to learn how few incidents there were in which the NSA managed to disrupt Tor. S that brought large sections of the network to a grinding halt. As it turns out, they're bark is much worse than their bite.

The thing is, most Tor users couldn't be bothered. But then most users aren't interested in running a hidden server just as most P2P users don't bother seeding. Most are hit n' run downloaders. They know that as U.S. citizens they stand a good chance of getting sued if they leave their balls out there long enough. So some users opt to not further their own security knowledge. Let the Tor devs do it, they say. Can't be bothered.

Except most of the Tor advice by Tor developers I've read come up woefully inadequate. In fact I find that they aren't paranoid nearly enough. It's always been my belief that you can never be sufficiently paranoid as far as protecting your freedom is concerned, since the powers that be want to capture it and bottle it the way a cancer captures control of a cell: One organelle at a time with little of it's environment aware of the slow-boiling attack. To be honest... I suspect they depend on apathy and ignorance. And a lot of users gladly oblige.

Mr. Frog, meet boiling pot of water...

So then, what can we do? Well for starters, we can get the right security mindset.

Tor and Your PC

A secure computer is your best defense as the NSA mostly relies on man-in-the-middle attacks and browser exploits that deliver payloads to hidden Tor servers. That said, you should anticipate and expect such an exploit can infiltrate your system at any point. Things like Nits (network bugs), you have to be aware of. Thus the need to adhere to the following:

- Use Linux whenever possible. Yes, I know you're comfortable using Windows and think Linux too much of a bother. But you won't if you're ISP is subpoenaed for something you said on Facebook. Something anti-feminist, for instance. So learn to use it.

If you're new to Linux, look at Linux Mint. If you're experienced, Debian is a good choice. Windows can't be trusted primarily because it is closed-source, but also because malware is more effective on it than Linux. If Linux is out of the question, consider Tails or Whonix as these apps come preconfigured to not allow any outgoing connections to clearnet.

Updating… stuff.

Your PC must also be updated, always. Not updating leads to vulnerabilities and exploits such as those in Windows. Optimally, you should ensure Tails is always updated each time you use Tor, and avoid any sites that use Java/Javascript/Flash or any kind of scripting as these execute code in ways you cannot see. Use these only in an emergency and never in your home system.

Situation Awareness

If an agency can monitor your local connection as well as the link you are browsing, then (with sufficient resources) they can apply traffic analysis to pinpoint your real location. Therefore, I recommend you do not use Tor in your residence 100% of the time.

Just to clarify, do not use Tor in your legal residence if doing any kind of covert work or anything illegal without strict security measures in place; the kind the average Tor user will likely overlook. Let that other guy learn his lesson. It's a tough break, but better him than you. He's a 19 year old named Jimmy who likes hacking. You're a 32 year old construction guy with two kids and a mortgage. Who has more to lose? Right, you. So study counter-surveillance and counter-forensics like your life depends on it... because it does!

For enemies of the state-level operations, I would suggest not engaging anything even near your online PC at home. Certainly nothing that makes you think you need Tor to hide it. It may be fine for private browsing but not for someone planning a coup, running an illegal operation (home bible study in Iran, for instance), or trying to disappear.

Be wary of using it in hotels as well, where often there are many cams watching with 24/hr surveillance. That location can be linked to Tor activity.

Do not use Tor more than a day in any specific location. A correlation-attack can be done in less than an hour if a black van is parked nearby--a van you will not see. They may not slap the cuffs on you as you walk out of the cafe that very week, but later they might. Consider the area a toxic dump after a day, regardless if you must travel to the next shop or town.

If you want to get really cloak and dagger about it, have an app running (an MMO, for instance) while you are out and about doing your Tor activity that makes it look like you were home during that time.

"We've been watching you Mr. Anderson, and it seems you've been living... two lives." -- Agent Smith, The Matrix

Darknet Personas

You've no doubt read of Tor busts where an undercover agent snagged a phone number or clearnet nic from someone they were targeting because said target trusted too much, too quickly. You can avoid this by retraining yourself, unlearning what you've learned.

You must consider your Tor sessions the property of your other Self. The cloned You - that shadowy thievish looking guy above. The second You. One that despises Incubus and loves Tool and views Neo as just another beta-orbiting punk who got the luck of the draw when Morpheus and crew unplugged him. This clone would not use Twitter or YouTube or other social gunk. He would never hang with you nor call you up for a few beers. In fact, he hates beer, preferring J&B as he hacks with John Carpenter's The Thing OST playing as mood music in the background. That's your other You. The smarter you.

And he must be the new You on Tor. And you must forever separate him from the non-Tor You.

His Facebook, Twitter and YouTube accounts are all fake, having never once used them on his home PC. His nics are different, as is his passwords, likes/dislikes and even the fonts he uses to browse the Deep Web. Mixing this dark persona with your own would be like the boy made of matter kissing the anti-matter girl...

BOOM.

Further, any phone calls this person makes is done by prepaid phones that were not purchased by any credit cards he holds. He is a cash n' carry guy and then only if he is twenty miles from home. Any SIM cards he uses are strictly used in conjunction with Tor activity and never used in phones the other guy uses. And... he deliberately leaves false info wherever he goes. Kinda like the CIA does.

But to better clarify this idea, let's assume John Doe doesn't know any better. He watches a movie on Netflix. Then he mosies on over to Freenet and drops intel without even realizing it, eager to share his great cinema experience with his darknet buds (no pun).

"Hey guys, just watched a cool flick with Russell Crowe. Kinda Michael Bay-ish and Liam Neeson's cameo was too short, but makes for a good flick if you want to learn how to disappear. But those police, sweet Jesus! Those rent-a-cop guys sure are as dumb as a sack of bricks!"

Police are dumb, he says.

Metadata is collected by Netflix just as it is with Google and Yahoo. Every single user. They know every film you viewed and even which ones you hated. He's even made forum posts indicating similar weather and, though not mentioning names, has griped about local politicians being handcuffed in very geo-specific arrests, even dropping the charges!

How many Netflix fans do you think watched this movie at the time of his Freenet post? How many in cities that had local politicians arrested for embezzling? How many with similar weather depicted in the film? Most likely less than ten. Maybe not even that.

There is also the handwriting element. Does he mispell the same words over and over? Throw commas like daggers? Misuse semi-colons and run-on sentences? System clock out of sync with his posts? All of this leads to a great profile that ties his IP address to his identity. Often it is enough to get a warrant if he so much as whispers that he's obtained any kind of contraband.

Unless of course, all of this info is tailor-made to fit the other You.

Bottom line: Learn from Snowden's mistakes. Take every company's claim of anonymity with a grain of salt. The proof is in the amount of arrests tied to said company or app. In the case of [Freenet](https://freenetproject.org/)... none.

But there is always a first time. Recall that they only have to get lucky once, which more often than not relies on your carelessness.

Tor Hidden Services - High Risk, High Reward

CNN along with FoxNews has been trumpeting the defeat of certain hidden services for a few years now. Services like Silk Road and Freedom Hosting, which I'm sure you've heard about. They are a easy target for the FBI since hidden services are not high on the list of priorities by Tor developers yet. Same for the NSA.

Both agencies know every trick and hack there is to know about running a hidden service. And so should you. This is not to say you need the expertise to match their team of super hackers, but that you need even more vigilance to run such a service than you do visiting such a service.

Priority number one is simple: if you run one, you must own one. They must not be run under somebody else's control if you can help it, because if that service is compromised, everyone goes down. That means total anonymity, 100% of the time with world-class jewel-thief stealth ability.

The Silk Road admin did not have this ability. In fact, looking through the online docs detailing the arrest, one gets the impression he was very lax in IT security procedure. He repeatedly made mistakes such that luck on the part of LE never really came into it at all. The guy was just sloppy.

First

Never, ever, ever run a hidden service within a VM that is owned by a friend or a Cloud space provider. Remember, all "The Cloud" is, is someone else's drive or network, not your own. Encryption keys can be dumped from RAM. And who owns the RAM?

Right. The Cloud provider. Lightning strikes and there goes your own anonymity as well as the anonymity of your visitors if they are lazy in their browser habits. The FBI delivered a "nit" (network investigative technique) this way to unpatched Tor Browser Bundles in 2013\. If, however, you own the machine, then it's a different story. But let's back up a few steps and assume you don't. How might you go about running it on a host system?

Well first off, you would need two separate physical hosts from different parties, both running in virtual machines with a firewall-enabled OS that only allows Tor network activity and nothing else.

The second physical host is the one the hidden service runs from, also VM'ed. Secure connections are enabled by IPSec. What's IPSec, you ask?

"IPSec is a protocol suite, for securing Internet Protocol (IP) communications by authenticating and encrypting each IP packet of a communication session. IPsec can be used in protecting data flows between a pair of hosts (host-to-host), between a pair of security gateways (network-to-network), or between a security gateway and a host (network-to-host)."

If an intruder agent tampers with anything, you will know about it and can shut down the service or move it to a safer place, and all while being a ghost in the machine. You can imagine how valuable this would be in North Korea.

If you were in that cesspool of a country, you would be more than a little paranoid if the server went down even for a few seconds. But you could always move it to a more secure location or even start over, and you might just want to since you would not know if a RAID failure had occurred or if some commie jackboot was sending a copy of the VM to the higher ups.

Second

If going the host route, you must ensure that remote-console is always available to you by the host, any time you want. You must do everything remotely, in fact, and change passwords frequently via https. I'd say once per day as paranoia in such a climate as North Korea would be good for your health.

Third

You must never, not even once, access the service from home. Not from your Nexus 7\. Not from your girlfriend's Galaxy Note. Not even via Tor from your backyard using your neighbor's WiFi. Using a VPN as well is risky unless you know what you're doing. Only access it via secure locations at least ten miles away from your residence. Overkill, some might say, but then there is no such thing as overkill in a gulag.

Fourth

Move the service on occasion. Again, look at any Youtube video on how snipers train to take out an enemy. They move place to place after each shot to conceal the true location from the enemy. How often is up to you. Once a week? Once a month? Personally I'd say every twenty-one days. You can never be too secure when running one of these.

The Death of Anonymity

Prime minister David Cameron went on record in January, 2015 to say he wanted to [outlaw](http://gizmodo.com/uk-prime-minister-wants-to-ban-messaging-apps-without-b-1679184681) all encryption-enabled messaging apps if the government cannot have backdoor keys to decrypt encryption. It would be like a farmer allowing easy entry to the henhouse to cougars as well as foxes. While on the campaign trail, he said:

"Are we going to allow a means of communications which it simply isn't possible to read? My answer to that question is: No, we must not."

While he referred to mostly chat programs like WhatsApp and what not, you can bet the ranch he was also talking about apps like PGP, Freenet and the discontinued Truecrypt. Regrettably, he used the Hebdo (cartoonist) attack as justification (don't they all use these to further Big Brother agendas?).

I see a similar trend evolving in Canada regarding VPN usage. New laws now require VPNs to identify customers who download copyrighted works like movies and games so that infringement notices (i.e. scare letters) get to the right person. That sounds rather just on the surface of it, because who wouldn't deny George Lucas's ability to make more Star Wars prequels? Art, you know.

But therein is the problem. Mainly it's that politicians forget how the internet actually works.

Doing what they dictate means VPN providers must retain access logs for 6 months, minimum. This alone pretty much guarantees a VPN's ability to sell anonymity services (privacy, actually) will dissolve, thus leading to massive losses as customers aren't stupid. They know when their privacy is being targeted. Let the exodus begin! (Government cookie parties)

They also know that VPNs assign shared IP addresses for customers. One might be yourself, there in your jammies sipping Rickard's Red while downloading the latest NiN video YouTube seemingly blocked, while the other user is Uncle Frick downloading something from the Usenet group guys-who-like-bouncing-pigtailed-girls-on-a-knee.

The only solution is to move out of Canada altogether.

But then, perhaps that is what the government wanted all along.

The saddest part isn't that none of this won't stop terrorism or copyright infringement, or that it will hurt most private encryption vendor's businesses or that only politicians will have encryption while the citizens have none. No, the saddest part is that we will have become the frog-in-the-pot who turns the oven on ourselves to maximum temperature and then slip back into the pot, and all because someone more powerful than you or I said it was the right thing to do.

Our world will become Bizarro World. Where right is wrong and light is dark and no one has security except for the agents of the new Matrix they will build. Where to be more secure is to be less secure as us peons go... because if the government says so, well, that must be the gospel truth because when's the last time a politician lied?

If you learn nothing else, remember two things: Backdoors are security holes in 100% of cases. The second one is like it: Anonymity and Privacy and the freedom that comes of it will only die if we let it.

Closing Thoughts

As you can see, the powers that be are actively targeting your ability to make choices about your own freedom. They work in baby steps. They think you're stupid. They think they can run your life better than you can. Only they can't. Did the NSA stop the attack on Charlie Hebdo, the French cartoonist? Did they stop 9/11? The bombings in Spain? A death from a thousand cuts, a little at a time, and before you know it you're feeling very light-headed but aren't quite sure why.

Believe me, putting off your security and peace of mind will be enough to fuel that tsunami of cancer they're building up one cell at a time. If you've read this book then you've already taken all the baby steps you need. You've dipped your big toe into that whirlpool and it's high time you jumped in. Don't procrastinate. You know how warm the water is. Wait too long and the water might get too cold. Worse still is that someone might just lock you out altogether.

Just remember: Always nourish a strong security mindset. Develop an ability to configure things logically and anticipate trouble way ahead of time, seeing weaknesses in your submarine before the water comes roaring in. If in doubt about this, watch the film 'The Abyss'. See how Bud reacts when the water comes roaring in? He panics! Most of the crew dies. Don't wait till that fateful day. Have something set up long ahead of time. A plan B. A plan C. Even a plan D if you can afford it.

Any intelligence agency has unlimited funding to kill freedom by censoring all of us - even censoring the freedom to buy what you want to buy. With the media in their back pocket they can conjure any boogeyman they want to run over you. It's not illegal for them to lie to you, but it is for you to lie to them. This hypocrisy costs them nothing but costs you everything, so like them, you must keep on top of changes to good security, updating as necessary and being on constant alert of new zero-day threats.

But if there is one thing that you have that they don't, it's the incentive to work harder than they do. They clock out at 5pm every day. Will you? The powers that be play dirty. And so should you.

Want to Know More?

First off, I owe you a big thanks and a round of beer for downloading this book. You could have picked any one of dozens of great books on this topic. You took a chance with mine. So thank you for that. Seriously, reading to the end takes a strong mind. If you liked what you read then I need your help! Please take a moment to leave a review for this book so others can learn to use Tor and Freenet and, well, protect themselves.

Speaking of protection, I've used a number of tools to get to where I'm at, and some of the topics that failed to pass the censors in this book quite miraculously managed to slip through in my other books. Go figure.

One thing though: when you have not one but two or three silver bullets to take down a werewolf, the better your chances of staying invisible to any other lycans roaming around out there. Mind you, I'm not prejudiced against those with Lycanthropy, as it is no laughing matter. But then neither is herd mentality.

So then. Don't use the same tools everyone else is using all the time. Mix it up a bit by checking out some other stuff of mine that did not see the light of day in this release:

Other Books You May Enjoy:

[Burners & Black Markets](https://www.amazon.com/dp/B01EU9A92K)

[Darknet: A Beginner’s Guide to Anonymity](https://www.amazon.com/dp/B008AP8TAK)

[The Invisibility Toolkit](https://www.amazon.com/dp/B014OMZ1N0)

[Tor & the Deep Web](https://www.amazon.com/dp/B075MBL4L2)

[3 in 1 Darknet Super Pack](https://www.amazon.com/dp/B06VY1MWMP)

[Usenet: The Ultimate Guide](https://www.amazon.com/dp/B0098DWUQW)

Coming:

Dark Linux

Cybercrime Supervillains

.