
## Appendix A • Implementing Cybercrime Detection Techniques on Windows and *nix

- Lists of spammers, harassers, mail bombs, and other e–mail abusers: www.ram.org/ramblings/philosophy/spam/spammers.html and www.spamhaus.org

## Honeypots, Honeynets, and Other "Cyberstings"

Although the strategy involved in luring hackers to spend time investigating attractive network devices or servers can cause its own problems, finding ways to lure intruders into a system or network improves the odds that you might be able to identify intruders and pursue them more effectively. A honeypot is a computer system that is deliberately exposed to public access—usually—for the express purpose of attracting and distracting attackers. Likewise, a honeypet is a network set up for the same purpose, where attackers will find not only vulnerable services, but also vulnerable routers, firewalls, and other network boundary devices, security applications, and so forth. In other words, these are the technical equivalent of the familiar police “sting” operation.

![](img/fd8e85097b37559dbc07dc22fd8cb1fe_226_0.png)

### Walking the Line between Opportunity and Entrapment

Most enforcement officers are aware of the fine line that they must walk when setting up a “sting”—an operation in which police officers pretend to be victims or participants in crime with the goal of getting criminal suspects to commit an illegal act in their presence. Most states have laws that prohibit entrapment; that is, law enforcement officers are not allowed to cause a person to commit a crime and then arrest him or her for doing it. Entrapment is a defense to prosecution; if the accused person can show that he or she was trapped, the result must be an acquittal.

Courts have traditionally held, however, that providing a mere opportunity for a criminal to commit a crime does not constitute entrapment. To entrap involves using persuasion, duress, or other undue pressure to force someone to commit a crime that the person would not otherwise have committed.

this holding, setting up a honeypot or honeynet would be like the (perfect legitimate) police tactic of flanking an abandoned automobile by the side of the road and watching it to see whether anyone attempts to burglarize, vandalize, or steal it. It should also be noted that entrapment applies only to the actions of law enforcement or government personnel. A civilian cannot entrap, regardless of how much pressure is exerted on the target to commit the crime. (However, a civilian could be subject to other charges, such as criminal solicitation or criminal conspiracy, for causing someone to commit a crime.)

The following characteristics are typical of honeypots and honeynets:

- Systems or devices used as lures are set up with "out of the box" default installations so that they are deliberately made subject to all known vulnerabilities, exploits, and attacks.

- The systems or devices used as lures include no real sensitive information—such as passwords, data, applications, or services on which an organization must rely depend or it must absolutely protect—so these lures can be compromised, or ever destroyed, without causing real damage, loss, or harm to the organization that presents them to be attacked.

- Systems or devices used as lures often contain deliberately tantalizing objects or resources, such as files named password.db, folders Top Secret, and so forth—consisting only of encrypted garbage data or log files of no real significance or value—to attract and hold an attacker's interest long enough to give a backtrace of identifying the attack's point of origin.

- Systems or devices used as lures also include or are monitored by passive applications that can detect and report on attacks or intrusions as soon as they start, the process of backtracing and identification can begin as soon as possible.

Although this technique can certainly help identify the wary and unsophisticated attacker, it also runs the risk of attracting additional attention or from savvy attackers. Honeypots or honeynets, once identified, are often publicized on hacker message boards or mailing lists and thus become more subject to attacks and hacker activity than they otherwise might. Likewise, if the organization that sets up a honeypot or honeynet is itself identified, its production systems and networks may also be subjected to more attacks than might otherwise be the case.

www.synergy.com

The honeypot technique is best reserved for use when a company or organization employs full-time IT security professionals who can monitor and deal with these lures on a regular basis, or when law enforcement operations seek to target specific suspects in a “virtual sting” operation. In such situations, the risks are sure to be well understood, proper security precautions, processes, and procedures are far more likely to already be in place (and properly practiced). Nevertheless, for organizations that seek to identify and pursue attackers more proactively, honeypots and honeynets can provide valuable tools to aid in such activities.

Numerous quality resources on honeypots and honeynets are available on the Internet by searching on either term at http://searchsecurity.techtarget.com or www.techrepublic.com. The Honeypot Project at www.honeynet.org is probably the best overall resource on the topic online; it not only provides copious information on the project’s work to define and document standard honeypots and honeynets, but it also does a great job of exploring hacker mindsets, motivations, tools, and attack techniques.

## Summary

Why is cybercrime detection important to investigators? Only by detecting that cyberimes have occurred (or are occurring) will investigators be able to get a step ahead of the criminals and start the investigation while the trail is still “hot.” Furthermore, only when suspicious activity is detected or observed investigators know what the steps necessary to obtain, secure, and prepare the evidence that will be necessary if any kind of legal charges are to stick. By following attack traffic from its targets back to its sources—even if those sources point only to victims and not the real attacker, as may be the case—investigators can work with service providers to inform them about and to help administrators and security personnel prevent such attacks from recurring. Even when prosecution is not possible, or when those who have been attacked decide not to pursue legal remedies, the information obtained and shared during the investigation can still have an overall positive impact on the security posture and awareness of various parties.

One key in obtaining evidence of cyberimes may be found by enabling auditing of suspicious events in the boundary devices and operating systems that are likely to be subject to attack. IT professionals should understand how to instruct these systems and devices to log data and should be aware of what kinds and classes of events are most worth logging. These events include log attempts, access to sensitive resources, use of administrative privileges, and monitoring of key system and data files. Likewise, law enforcement professionals should be aware not only that these logs exist, but also that they provide the most salient evidence of attempted or successful cyberimes, and they must be aware of how to make appropriate efforts to secure and protect these logs before and during the investigation. Firewalls, routers, proxy servers, network servers, and IDSes can all contribute logs (plus related reports, alerts, and alerts) to substantiate allegations that unauthorized access, alteration, destruction, or denial of service occurred for information assets and services and, in some cases, to track back the origin of the activity.

In the security model known as triple-A (authentication, authorization, and accounting), accounting is what makes auditing and logging of suspicious or illicit activity possible. IT and law enforcement professionals alike must understand this concept. Administrators must practice proper auditing and logging techniques to make sure they can detect cybercrimes (preferably before they succeed at compromising or damaging an organization’s IT assets or infrastructure), obtain evidence that can help
