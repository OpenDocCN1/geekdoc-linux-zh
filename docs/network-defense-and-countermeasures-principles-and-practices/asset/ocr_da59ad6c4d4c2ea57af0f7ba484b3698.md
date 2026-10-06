# CHAPTER 11 Security Policies

FYI: The “CIA” Triad

No, this is not a nefarious plot, nor does CIA stand for Central Intelligence Agency in this instance. CIA is an acronym for Confidentiality, Integrity, and Availability. This has direct bearing on access to resources. The concept is that data must be kept confidential. That means only those personnel with a need to know will access to the data. Secondly, the data integrity must be maintained. That means the data must be reliable. That involves limiting who can alter the data and under what conditions they can alter it. Finally, all data must be available to be accessed.

It is worth keeping this acronym in mind when thinking about access control. Your goal is to make sure the data is accurate, confidential, and available only to authorized parties.

This is where the least privileges come into play. The idea is simple. Each user, including IT personnel, gets the least access they have to effectively do his job. Rather than asking the question “Why not give this person access to X?” you should ask “Why give this person access to X?” If you do not have a very good reason, do not provide the access. This is one of the fundamentals of computer security. The more people who have access to any resource, the more likely breach of security is to occur.

Clearly tradeoffs between access and security must be made. One common example involves sales contact. Clearly a company's marketing department needs access to this data. What, if competitors get all of your company's contact information? That information could allow them to begin targeting your current client list. This requires a tradeoff between security and access. In this case you would give sales access only to the contacts that are within their territory. No one other than the sales manager should have complete access to all contacts.

# Defining Developmental Policies

Many IT departments include programmers and/or web developers. Unfortunately many security policies do not address security programming. No matter how good your firewalls, proxy server, scanning, and policies, if your developers create code that is flawed you will have security breaches. Clearly the topic of security programming requires a separate volume to explore thoroughly. Nonetheless, if your company currently has no security programming initiatives, this checklist is certainly better than developing in a vacuum. It also serve as a starting point to get you thinking, and talking, about secure programming.

+   - All code, especially code done by outside parties (contractors, consultants, etc.) must be checked for back doors/Trojan horses.

+   - All buffers must have error handling which prevents buffer overflows.