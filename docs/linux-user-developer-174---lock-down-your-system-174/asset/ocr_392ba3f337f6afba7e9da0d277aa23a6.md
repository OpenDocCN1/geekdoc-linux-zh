# **THE CIA TRIAD**

**Confidentiality**

When discussing InfoSec, it is a given that private data should be just that. Confidentiality encompasses obvious steps to keep data safe such as storing it offline, encryption and use of 2FA (two-factor authentication).

Confidentiality also pertains to people. Anyone with access to sensitive data should be trained to avoid security risks by choosing strong passwords, being aware of getting hacked themselves through social engineering, and having clear privacy guidelines to follow.

**Integrity**

Integrity involves ensuring data is consistent and accurate, both when stored and transmitted. Simpler ways of ensuring this involve setting file permissions and user access controls. More advanced methods may involve use of cryptographic checksums such as MD5 to produce a hash value of a new document to compare to the previous copy.

Integrity also encompasses running and maintaining backups of all important data. This is crucial to protect against data loss caused by factors other than unsavourious hackers, such as a server crashing due to an update or a hardware fault.

**Availability**

Availability focuses on making sure that data is accessible at all times regardless of outside influences (like hacking or natural disasters).

This may involve using RAID drives to make sure there are several copies, or storing backups on a separate site to make them easier to restore. Availability is better ensured by keeping all software up to date, as well as making sure hardware repairs are carried out rapidly. For data stored on servers, availability also involves providing enough bandwidth to all users to avoid slowdown caused by bottlenecks.

H

**ardening. Penetration. Remote exploits. Least privilege. The number of buzzwords and terms related to InfoSec (information security) is almost as great as the various tools out there, each of which boasts that it'll analyse your network for any potential threat and/or secure it against hackers.**

In this guide, we will examine some of the network security community's favourite tools as well as detail the specific threats they address.

One of the central tenets of network security is to reduce your ‘attack surface’ through removing unnecessary software. For this reason, any tools listed here should be run from within a pen-testing distribution of Linux, such as Kali, wherever possible.

Before proceeding, make sure you have followed other basic InfoSec best practices, too. Do your network devices have any pre-installed accounts with default passwords that a hacker could exploit? Do the accounts you have installed all require admin privileges to make systemwide changes?

Finally, make sure you are aware where your server's log files are located. Usually they can be found in **/var/log**. These can be invaluable when simulating an attack on your network.

![](bbox=[0.08, 0.21, 0.69, 0.58])

> “One of the central tenets of network security is to reduce your ‘attack surface’ through removing unnecessary software”