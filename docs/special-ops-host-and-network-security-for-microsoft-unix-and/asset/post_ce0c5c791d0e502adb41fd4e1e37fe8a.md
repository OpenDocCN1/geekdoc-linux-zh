
## Chapter 17 • Architecting the Human Factor

from Hank Strossen the unfortunate Schaumsburg incident, yet here was a message from Hank with the subject, “Important Message From Hank Strossen”. Steve had “Important Messages” from Cheryl Fitzpatrick and Mario Andres to boot.

Steve knew instinctively something wasn't right about this. Four messages with the same subject meant a prank—one of the IT guys had sent out these messages as a reminder to shut down your workstation, or at least use a password-protected screensaver. Such pranks were not uncommon—Steve thought back to the morning he'd come into the office to find his laptop had been stolen, only to find that an IT manager had taken hostage since it wasn't locked down.

Steve clicked the paperclip to open the attached document, and soon he immediately closed the word processor. He made a note to contact IT when they got in (probably a couple of hours from now) and pulled up a spreadsheet he'd been working on. While he worked, more and more of the messages popped up in his mailbox as Steve’s coworkers and the eastern seaborn began reviewing their e-mail. By 8:15 A.M., the corporate mail servers became overwhelmed with Melissa instances, and the message stores began to fail. In order to stop the rampant spread of the virus, the mail servers were pulled from the network, and business operations ground to a halt.

Although it could be argued that Steve (and each of his co-workers) had to open the message attachment to activate the virus, their involvement was active, Melissa was socially engineered to take advantage of normal user behavior. Since the body of the message didn't contain any useful content, the user would open the attachment to see if there was anything meaningful within. When confronted with a full document of links to pornographic Web sites, the user would simply close the document and not mention it of of embarrassment.

### Study 2: Samind/IIS Worm

In May of 2001, many Microsoft IIS Web site administrators began to find their Web sites being faced with an anti-United States government slogan and an e-mail address within the yahoo.com. domain. It rapidly became clear that a new worm had entered the wild, and was gaining great success in attacking Microsoft servers.

Chris Noonan had just started as a junior-level Solaris administrator with a large consulting firm. After completing orientation, one of his first tasks was to build his Solaris Ultra-10 desktop to his liking. Chris was ecstatic, to a previous

![](img/729efc56f204a2ebffb8295c3a2dfdfb_914_0.png)

job he had deployed an entire Internet presence using RedHat Linux, but he'd been working with an old Sparc 5 workstation he'd purchased from a friend, he'd been able to get this new job working with Solaris systems. Chris spent much of the day downloading and compiling his favorite tools, and getting comfortable with his new surroundings.

By midday, Chris had configured his favorite Web browser, shell, and terminal emulator on his desktop, and spent lunching some security Web sites for new tools he might want to load on his system. On one site, he found a post with source-code for a Solaris buffer overflow against the Sun Solstice AdminSuite RPC program, samind. Curious, and looking to score points with his new employers, Chris downloaded and compiled the code, and ran it his own machine. With a basic understanding of buffer overflows, Chris hoped the small program would provide him with a privileged shell, and then later this afternoon he could demonstrate the hack to his supervisor. Instead, after announcing “buffer-overflow sent,” the tool seemed simple. Disappointed, Chris deleted the application and source code, and continued working.

Meanwhile, Chris's system began making outbound connections on TCP/80 and TCP/111 to random addresses both in and out of his corporate network. A new service had been started as well, a root-shell listener on TCP/600, and his .hosts file had been appended with “+ +-”, permitting the use of rtoools to any host that could access the service port on Chris's system.

Later in the afternoon, a senior Solaris administrator sounded the alarm that a worm was present on the network. A conjob on his workstation alerted him begun listening on port 600, and he quickly learned from the syslog that his samind task had crashed. He noticed many outbound connections on port 111, and the network engineers began sniffing segments for other systems making similar outbound connections. Altogether, three infected systems were identified and disconnected, among them Chris's new workstation. Offline, the creation times of the alternate inetd configuration file were compared for each system, and Chris's system was determined to be the first infected. The next day, the worm was found to have been responsible for two intranet Web server defacements, and two very irate network-abuse complaints had been filed from the ISP for their Internet segment.

This sequence of events represents the best-case scenario for a Solaris/IIS worm. In most cases, the Solaris hosts infected were workhorse machines, not subject to the same sort of scrutiny as the administrator who found the new listening port. The exploit that the worm used to compromise Solaris systems was over two years old, so affected machines tended to be neglected

![](img/729efc56f204a2ebffb8295c3a2dfdfb_915_0.png)

NTP server or fragile application servers admins were reluctant to keep up-to-date with patches. Had it not been for the worm's noisy IIS server defacement, this worm may have been quite successful at propagating quietly to dormant, triggering on a certain time or by some sort of passive network activation, such as bringing down a host that the worm has been pinging at specific intervals.

In this case, Chris's excitement and efforts to impress his new co-workers led to his willful introduction of a worm. Regardless of his intentions, Chris actively obtained hostile code and executed it while on the corporate network, leading to a security incident.

### The State of Internal Security

Despite the NIPC statistics indicating that the vast majority of losses incurred by information security incidents originate within the corporate network, security administrators at many organizations still follow the "exoskeleton" approach to information security, continuing to devote the majority of their time to fortifying the gates, paying little attention to the Web of sensitive systems throughout their internal networks. This concept is reinforced by every worm and virus that—since security threats start outside of the organization, the damage can be prevented by ensuring they don't get inside.

The exoskeleton security paradigm exists due to the evolution of the network. When worms were first deployed in commercial environments, hackers and viruses were more or less the stuff of science fiction. Before the Internet became a business requirement, a wide-area network (WAN) was actually a collection of point-to-point virtual private networks (VPNs). The idea of an employee having havoc on his own company's digital resources was laughable.

As the Internet grew organizations began joining public networks to their previously independent systems, the media began to distribute stories of the "hacker", the unshaven social misfit-addict whose technical genius was devoted entirely to ushering in an anarchy by manipulating traffic on the informationhighway. Executive orders were issued, and walls were built to protect the organization from the inhabitants of the digital jungle that existed beyond the phone closet.

The end result of this transition was an isolationist approach. With a firewall defending the internal networks from intrusion by external interests, the organization was deemed secure. Additional security measures were limited to defining

access rights on public servers and ensuring e-mail privacy. Internal users were not viewed as the same type of threat as the externals beyond the corporate firewalls, the same deterrents were not necessary to defend against them.

Thanks in large to the wake-up call from the virus incidents of the past few years, many organizations have begun implementing some programs and controls to bolster security from the inside. Some organizations have even begun to apply the exoskeleton approach to some of their sensitive departments, using techniques that we will discuss in the section, "Securing Internal Networks." But largely, the exoskeleton approach of "crunchy outside, chewy center" is still the norm.

The balance of security and usability generally follows a trend like a teeter-totter—at any time, usability is increasing and security implications are not counted, and the balance shifts in favor of usability. This makes sense, usability follows the pace of business while security follows the pace of the threat. Periodically, a substantial new threat is discovered, and security countermeasures brings the scales closer to even. The threat of hackers compromising networks from the public internet brought about the countermeasure of firewalls and exoskeleton security, and the threat of autonomous code brought about the introduction of anti-virus components throughout the enterprise. Of course, adding to the security side of the balance can occasionally have an effect on usability, as you'll see in the next section.

### User Community Response

Users can be like children. If a toddler has never seen a particular toy, he is totally indifferent to it. However if he encounters another child playing with a Tickle-Me-Elmo, he begins to express a desire for one of his, in his unique fashion. Once, he has got his own Tickle-Me-Elmo, he will not give it up without a severe tantrum ensuing.

The same applies to end users and network access. Users quickly blur the line between privileges and permissions when they have access to something they enjoy. During the flurry of mail-borne viruses in 1999 and 2000, some organizations made policy changes to restrict access to Web-based mail services such as Gmail to minimize the ingress of mail viruses through uncontrolled systems. At one company I worked with, this touched off a battle between users and gateway administrators as the new restrictions interrupted the normal course of business. Regardless of the fact that most users'Web-mail accounts were of a purely personal nature, the introduction of filters caused

![](img/729efc56f204a2ebffb8295c3a2dfdfb_917_0.png)
