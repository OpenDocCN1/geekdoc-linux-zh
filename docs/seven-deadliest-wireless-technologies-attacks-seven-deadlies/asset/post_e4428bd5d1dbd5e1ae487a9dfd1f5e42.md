
![](img/fa764b70be0fdcb44b75286d4f8589e2_39_0.png)

## FIGURE 1.11

GenPMK Computing a Hash File

![](img/fa764b70be0fdcb44b75286d4f8589e2_39_1.png)

## FIGURE 1.12

CoWPAtty Using a Precomputed Hash File Instead of a Dictionary

In Figure 1.12, doing a live crack onsite would have been done in about 37 s. Using a hash file, which could be computed ahead of time in off hours or down time or from one of the publicly available sets, the lookups were done in 0.06 s. Quite the time savings, if you end up reusing the hash file several times.

Recent developments have helped improve the process of doing the computationally heavy portions of WPA cracking and hash table generation. The usage of Field Programmable Gate Arrays (FPGAs), which are programmable processors, has shown a much faster SHA1 implementation than on generic CPUs since the algorithm is built into the hardware itself. This means that the FPGA does only one thing and it does very fast. Additionally, recent advances in video card Graphics Processing Units (GPUs) from companies like Nvidia and ATI have allowed non-video processes to be run on their chips. These chips are much better suited for the type of computations being performed. A sample implementation is available at http://code.google.com/p/pyrit/

## SUMMARY

While WPA-PSK (and WPA2-PSK) is an improvement over WEP, by creating a simpler method for users to remember and enter passphrases, the IEEE introduced a human flaw into the equation. WPA-PSK has a 256-bit key, much more substantial than WEP's 128-bit offering, and the randomness of that key is based on a user's ability to choose a random passphrase and a unique SSID, which in general, people are not very good at.

In short, it's all down to choosing a good passphrase. There have been no reports of WPA-PSK passphrases being cracked with such an attack; however, there's really no way to detect it being done. Anecdotally from professional pen testers though, usage of the Church of Wi-Fi tables has enjoyed about a 50 percent success rate if the SSID is in the list, meaning that an attacker has a decent chance of being able to walk into a situation and being able to crack a password. It just goes to show that if you use WPA-PSK, you had better follow the IEEE's advice from the standard and use a 20-character passphrase that is not based on any dictionary words, and is made up of uppercase and lowercase letters, numbers, and a few symbols for good measure.

Other measures to reduce your risk of a brute force attack on WPA:

- Periodically changing passphrases (maintaining length and randomness)
- Periodically changing the SSID, thus changing the salt value
- If sensitive or financial data is being sent, consider the installation and use of a Wireless Intrusion Detection System (WIDS)
- If at all possible, migrate to a WPA-Enterprise solution
- Educate your users on the need for complex passphrases

## Endnotes

1. www.netstumbler.org/t22/faq-legalities-concerning-wardriving-netstumbling-nethugging-6430/#post48649; [retrieved 01.12.09].
2. http://standards.ieee.org/getieee802/download/802.11i-2004.pdf; [retrieved 01.12.09].

## Wireless – Client Attacks

### INFORMATION IN THIS CHAPTER

- Public Hotspot Dangers
- How Hotspots Work
- Attacking Public Hotspots
- The Crux of the Problem
- Solutions
- Injection Attacks

Wireless network security is getting better. When wardriving first hit in 2001, statistics showed only about 30% of access points were secured with some sort of encryption. Today that number is close to 70%, indicating that people are slowly getting better at securing their access points. Since then, wireless client devices have become a tempting target for attackers. Workers become increasingly mobile and depend on wireless network access at the office and on the road. The availability of public hotspots has the general public becoming more and more accustomed to Internet access being available at every coffee shop, airport, and hotel they might travel to.

Client security is often overlooked as users often think of it when connecting to the "home" network. In reality, clients are sometimes more of a tempting target since they can be attacked away from watchful eyes of information technology (IT) departments and often can contain just as much valuable information or be useful entry points into the network.

In early 2006, Simple Nomad of the Nomad Mobile Research Center (NMRC) presented a talk at Shmoocon in Washington, D.C., outlining his experiences in a talk entitled "Hacking the Friendly Skies." In his talk, he detailed the many ways he was able to access the private documents and manipulate the information on laptops in use at 30,000 ft on cross-country flights. His discoveries and techniques showed that he was able to find at least one vulnerable target on every flight he tested on, often without any indication or interaction with the user. His actions showed that every executive in the first class with a laptop is a potential target, even in more unusual environments, far away from the watchful eye of IT administrators (www.nmrc.org/pub/present/shmoocon-2006-sn.ppt).

Vacationers at hotels are often a tempting target. There is no guarantee that the hotel-named hotspot you are connecting to is actually the hotel’s network. Take the case of the Defcon 16 hacker conference at the Riviera Hotel and Casino in Las Vegas in 2008. Before the convention, there were 12 access points detectable from the pool with the hotel’s network Service Set Identifier (SSID). After the first day of the three-day conference, there were 130 access points available. Some odds at casinos are more in your favor than others, and a hapless traveler connecting to a legitimate access point is not one of them.

## PUBLIC HOTSPOT DANGERS

Just about everyone is familiar with the idea of public Wi-Fi hotspots. Every coffee shop seems to have one, as well as restaurants, bars, grocery stores, airports, and hotels. Hotels, in particular, are nearly required to have wireless Internet access to stay competitive and, with today’s seemingly endless flight delays, airport wireless is probably the only thing keeping business travelers from staging a revolt.

What most people don’t seem to think about are the inherent dangers of bringing a computer onto a random network that you have no reason or way to verify or trust. Would you haul a desktop computer around and connect it to any random network cable that you found lying around? Of course not (for reasons other than the obvious hauling problems), yet people connect their mobile wireless devices to seemingly random networks all the time without thinking about who else might be on the same network.

From an attacker’s perspective, the neighborhood coffee shop where all the customers hang out on sofas with laptops is a prime ground for targeted fraud and abuse of wireless clients. Hotels hosting conferences are also a very tempting target.

## HOW HOTSPOTS WORK

There is no set standard for public hotspots. They are designed around a business model rather than a technical model. Their main purpose is to draw in and get customers to stay long enough to order a second (or third) cup of coffee.

In the early days of wireless, it was as simple as the owner running a digital subscriber line (DSL) or other high-speed line into the business and plugging in an open access point. This worked great: customers could just connect with no issues. Shortly thereafter the inevitable happens and all the neighboring homes and businesses notice the new open network and proceed to use it freely without purchasing anything from the owner. After a short time, legitimate users complain about the slow speed, and the owner figures out that there are a few dozen extra users on the system than in the business. They then proceed to enable encryption and put up a sign for customers to ask for the password to use the wireless. This works for a while until the neighbors figure out that they can go in and buy the cheapest thing on the menu and
