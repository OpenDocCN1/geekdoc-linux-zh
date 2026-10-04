
Without logs, the technical support would be just as useless and clueless as the confused client calling them to solve a problem. Nobody in the company would know how to start fixing a simple DNS lookup problem, let alone mysterious routing issues involving packet loss, preferred routes, and other networking witchcraft. Many VPN providers feel obliged to vociferously defend their log-less service to keep up with competitors making similar claims, but this is a falsehood that has led to a pointless race to the bottom, powered by blatant lies—or “marketing,” as I believe they call it these days.

The best you can hope for from a VPN provider is that they do not sell customer data to the highest bidder. Don’t even bother with free providers. Invest in your privacy, both in time and money. I recommend starting with AirVPN and ProtonVPN, which are both serious actors in the business.

This same perception of anonymity applies to Tor (The Onion Router, https://www.torproject.org), which promises anonymous passage through the internet via a network of nodes and relays that hide your IP address. Is there any reason you should blindly trust that first node you contact to enter the Tor network any more than the unsolicited phone call promising a long-lost inheritance in exchange for your credit card number? Sure, the first node only knows your IP address, but maybe that’s too much information already.

## Location, Location, Location

One way to increase your anonymity is to be careful of your physical location when hacking. Don’t get me wrong: Tor is amazing. VPNs are a great alternative. But when you do rely on these services, always assume that your IP address—and hence, your geographical location and/or browser fingerprint—is known to these intermediaries and can be discovered by your final target or anyone investigating on their behalf. Once you accept this premise, the conclusion naturally presents itself: to be truly anonymous on the internet, you need to pay as much attention to your physical trail as you do to your internet fingerprint.

If you happen to live in a big city, use busy train stations, malls, or similar public gathering places that have public Wi-Fi to quietly conduct your operations. Just another dot in the fuzzy stream of daily passengers. However, be careful not to fall prey to our treacherous human pattern-loving nature. Avoid at all costs sitting in the same spot day in, day out. Make it a point to visit new locations and even change cities from time to time.

Some places in the world, like China, Japan, the UK, Singapore, the US, and even some parts of France, have cameras monitoring streets and public places. In that case, an alternative would be to embrace one of the oldest tricks in the book: war driving. Use a car to drive around the city looking for public Wi-Fi hotspots. A typical Wi-Fi receiver can catch a signal up to 40 meters (~150 feet) away, which you can increase to a couple hundred meters (a thousand feet) with a directional antenna, like Alfa Networks’ Wi-Fi adapter. Once you find a free hotspot, or a poorly secured one that you can break into—WEP encryption and weak WPA2 passwords are not uncommon and can be cracked with tools like Aircrack-ng and Hashcat—park your car nearby and start your operation. If you hate aimlessly driving around, check out online projects like WiFi Map, at https://www.wifimap.io, that list open Wi-Fi hotspots, sometimes with their passwords.

Hacking is really a way of life. If you are truly committed to your cause, you should fully embrace it and avoid being sloppy at all costs.

## The Operation Laptop

Now that we have taken care of the location, let’s get the laptop situation straight. People can be precious about their laptops, with stickers everywhere, crazy hardware specs, and, good grief, that list of bookmarks that everyone swears they’ll go through one day. That’s the computer you flash at the local conference, not the one you use for an operation. Any computer you use to rant on Twitter and check your Gmail inbox is pretty much known to most government agencies. No number of VPNs will save your sweet face should your browser fingerprint leak somehow to your target.

For hacking purposes, we want an ephemeral operating system (OS) that flushes everything away on every reboot. We store this OS on a USB stick, and whenever we find a nice spot to settle in, we plug it into the computer to load our environment.

Tails (https://tails.boum.org/) is the go-to Linux distribution for this type of usage. It automatically rotates the MAC address, forces all connections to go through Tor, and avoids storing data on the laptop’s hard disk. (Conversely, traditional operating systems tend to store parts of memory on disk to optimize parallel execution, an operation known as swapping) If it was good enough for Snowden, I bet it’s good enough for almost everyone. I recommend setting up Tails OS and storing it on an external drive before doing anything else.

Some people are inexplicably fond of Chromebooks. These are minimal operating systems stacked on affordable hardware that only support a browser and a terminal. Seems ideal, right? It’s not. It’s the worst idea ever, next to licking a metal pole in the wintertime. We’re talking about an OS developed by Google that requires you to log in to your Google account, synchronize your data, and store it on Google Drive. Need I go on? There are some spinoffs of Chromium OS that disable the Google synchronization part, such as NayOS, but the main point is that these devices were not designed with privacy in mind and under no circumstances should they be used for anonymous hacking activities. And if they were, then launch day must have been hilarious at Google.

Your operation laptop should only contain volatile and temporary data, such as browser tabs, a copy-paste of commands, and so on. If you absolutely need to export huge volumes of data, make sure to store that data in an encrypted fashion on portable storage.

## Bouncing Servers

Our laptop's only purpose is to connect us to a set of servers that hold the necessary tooling and scripting to prepare for our adventure: the bouncing servers. These are virtual hosts we set up anonymously, only connect to via Tor or a VPN, and trust to interact with our more malicious virtual machines (VMs) and store our loot.

These servers provide us with a reliable and stable gateway to our future attack infrastructure. To connect to a bouncing server, we would SSH into it directly after ensuring our VPN or Tor connection is established. We can initiate a Secure Shell (SSH) connection from a random machine in a cold and busy train station and find ourselves a warm and cozy environment where all our tooling and favorite Zsh aliases are waiting for us.

The bouncing servers can be hosted on one or many cloud providers spread across many geographical locations. The obvious limitation is the payment solution supported by these providers. Here are some examples of cloud providers with decent prices that accept cryptocurrencies:
- RamNode (https://www.ramnode.com/) costs about $5 a month for a server with 1GB of memory and two virtual CPU (vCPU) cores. Only accepts Bitcoin.
- NiceVPS (https://nicevps.net/) costs about €14.99 a month for a server with 1GB of memory and one vCPU core. Accepts Monero and Zcash.
- Cinfu (https://www.cinfu.com/) costs about $4.79 a month for a server with 2GB of memory and one vCPU core. Supports Monero and Zcash.
- PiVPS (https://pivps.com/) costs about $14.97 a month for a server with 1GB of memory and one vCPU core. Supports Monero and Zcash.
- SecureDragon (https://securedragon.net/) costs about $4.99 a month for a server with 1GB of memory and two vCPU cores. Only accepts Bitcoin.

Some services, like BitLaunch (https://bitlaunch.io/), can act as a simple intermediary. BitLaunch accepts Bitcoin payments but then spawns servers on DigitalOcean and Linode using its own account (for three times the price, of course, which is downright outrageous). Another intermediary service with a slightly better deal is bithost (https://bithost.io/), which still takes a 50 percent commission. The trade-off, on top of the obvious rip-off, is neither of these providers gives you access to the DigitalOcean API, which can help automate much of the setup.

Choosing a cloud provider can come down to this bitter trade-off: support of cryptocurrencies and the pseudo-anonymity they grant versus ease of use and automation.

All major cloud providers—AWS, Google Cloud, Microsoft Azure, Alibaba, and so on—require a credit card before approving your account. Depending on where you live, this may not be a problem, as there are many services that provide prepaid credit cards in exchange for cash. Some online services even accept top-up credit cards with Bitcoin, but most of them will require some form of government-issued ID. That's a risk you should carefully consider.
