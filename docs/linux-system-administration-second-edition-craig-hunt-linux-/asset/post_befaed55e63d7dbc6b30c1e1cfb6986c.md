
# Part IV: System Optimization and Improvement

## Chapter List

- Chapter 15: Security
- Chapter 16: Performance Tuning
- Chapter 17: Making Your Job Easier with Scripts
- Chapter 18: Troubleshooting Your Linux System

## Featuring

- Common types of attacks on network security
- Authorization and authentication techniques
- Firewalls and other security techniques
- Benchmarks and elements of performance
- Performance tuning and eliminating bottlenecks
- Bash shell scripting
- Administrative scripting in other languages
- General troubleshooting techniques
- Troubleshooting specific problems

# Chapter 15: Security

## Overview

Monitor any Linux mailing list for a week or two, and you will see posts from someone whose system has been broken into or taken down by an unauthorized entry. You can tell from the tone of the messages that this is a frustrating experience. As a result, seasoned system administrators are always on the watch for holes in their security plan. They know that, as system administrators, they must constantly look for ways to improve security because there are always people outside looking to crack their security; if the system’s security stays as it is for too long, different cracking techniques can be tried until one eventually succeeds. If your security method changes over time, would-be intruders will need to spend most of their time trying to get back to the point they last reached, and the system will remain secure.

With all of the news stories of crackers being indicted, most people know that breaking into a computer system is illegal. Still there are many people who access the Internet with this goal in mind. Some are malicious, and others are just curious. What most of the world calls “hackers” can be divided into three categories: crackers, hackers, and script-kiddies.

Crackers are highly skilled computer users who intentionally break security on computer systems in order to cause damage and demonstrate superior ability. (The term was coined around 1985 by hackers to make a distinction between themselves and the destructive crackers.) A cracker is malicious, breaking into a system solely to cause damage and show superior ability. Crackers tend to steal information, use your identity to distribute spam, deny you access to your own system, and generally wreak havoc on your system. For many crackers, it is a game; others recognize that they can gain financially from their theft. To crackers, destruction is of no consequence. Their intrusion may not be obvious because they plan to be back or to use the system to relay mail, thereby disguising their identities. Crackers are the reason you need to check your system’s logs on a daily basis and to watch for the telltale signs we’ll discuss later in this chapter.

A hacker is a particularly skilled programmer who loves to hack around on computers. This person enjoys looking to learn new things and generally gets a rush out of even the smallest computer discovery. There are a great many of us out there. A hacker may fall into the cracker category, but not all hackers are crackers. In fact, the crackers probably make up a very small percentage. Most hackers do not crack systems—not because they can’t, but because they are not malicious. Hackers don’t break into systems to cause damage, but they may break in to learn how it is done or to test security for a colleague or client. We know some hackers who have broken into systems to learn how to protect them from intrusion. After breaking in, they leave the system undamaged and pass on information about the security flaw or create a patch to fix it.

There are numerous sites on the Internet that detail how to exploit known security flaws and provide scripts designed to do just that. Script-kiddie is the term commonly used to describe those who do not possess the skills required to break into a system on their own but instead download a script to perform the task. Often these break-ins are characterized by minor damage, since script-kiddies don’t usually know the system well enough to know what would cause damage. They do try to make themselves known to the target system’s administrator by leaving a calling card in the form of a file with a name that will be noticed or by changing the banner printed above the login (/etc/issue) to something offensive. Script-kiddies generally strive to make their intrusion known since they have no real skills to do further damage at a later date.

## Types of Attacks

There are so many types of security attacks that it is impossible to list all the variations. We explain some of the most common here, with the emphasis on clarifying how the attack is made and what vulnerability it attempts to exploit. It is important to say that there is no such thing as absolute security from these attacks. Even if there were, some enterprising cracker would soon find something else to exploit. This is true not only of Linux but of every operating system out there: all Unix versions, all Microsoft Windows versions, VMS, and any other operating system you can think of.

The goal is to maintain the highest possible level of security on your system by keeping up with new attacks as they hit. Watch your distribution's home site for updates that fix security exploits, and install them immediately. Each major distribution of Linux has a security–announce list where users and staff post news of new security exploits and other security–related news. Be sure to subscribe to the appropriate security list to stay ahead of would–be intruders.

## Trojan Horse

You probably remember the story of the Trojan horse from Homer's *Iliad*. The Greeks sent a giant wooden horse as a present to end their ten–year war with Troy. When it was within the gates of Troy, Greek soldiers emerged from inside and defeated the unsuspecting Trojans.

In security, then, a Trojan horse is a program or a script that is hidden inside an authorized program. This code, when executed, causes an undesirable effect. Many of these are aimed at Microsoft machines, targeting their mailers. For example, you may remember the "Love Bug" Trojan horse from May of 2000. It appeared to be an e–mailed love letter but, when opened, it would cause problems, such as sending itself to everybody on your e–mail address book, erasing your files, and downloading another Trojan horse program that would steal your passwords. This particular Trojan horse affected only Microsoft Windows machines; while Trojan horses are rare on Linux machines, they are not unheard of. In January of 1999, a Trojan horse was found in the util–linux–2.9g.tar.gz on some Web sites. This type of attack is difficult to protect against. As a result, Red Hat and many other distributions have begun adding checksums or Pretty Good Privacy (PGP) signatures to the packages they make available for download. Make use of these verification techniques if they are available to you.

## Pretty Good Privacy (PGP)

Pretty Good Privacy is a software package that provides both asymmetric data encryption, which is usually used for e–mail, symmetric encryption for other files, and secret key management. PGP is generally used to ensure that the e–mail you receive is as its author intended. Mail sent through the Internet can easily be intercepted, changed, or created as if it were from someone else entirely. With PGP, you can digitally sign your e–mail, generating a mathematical value based on your e–mail's content as encrypted using your private key. If the recipient of e–mail has your public key, the PGP software makes the same calculation, thereby determining that the message has not been altered. Since only you have the private key that encrypted the hash value that was successfully decrypted with your public key, only you could have digitally signed the e–mail. Packages made available for download may be signed the same way.

The difficulty comes with obtaining the public key in such a way as to be sure that the person who claims the key actually is the one who generated it. The most secure way is to meet face to face with the person, exchanging identification and public keys at the same time. Retrieving a signed software package from a Web site is not as secure. Typically you obtain the developer's key from a
