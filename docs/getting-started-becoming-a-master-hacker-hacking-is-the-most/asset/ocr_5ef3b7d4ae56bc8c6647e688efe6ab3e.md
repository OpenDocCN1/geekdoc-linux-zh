issue (for more on the new Metasploit evasion modules, read <https://www.hackers-arise.com/post/2019/03/27/metasploit-basics-for-hackers-part-24-the-new-evasion-modules-in-metasploit-5>).

# How Antivirus Software Works Before we begin to work toward an undetectable payload, we need to understand how anti-virus software works. Most AV software can detect malicious code by comparing signatures (code snippets and other artifacts) of known malware against software that is entering the system (for more on how antivirus software works, go to <https://www.hackers-arise.com/single-post/2016/10/28/Evading-AV-Anatomy-of-

<ClamAV>. Although some software developers have begun to use heuristic techniques (detecting known malicious behavior) this is still not widespread among AV applications as it requires significant CPU

cycles to incorporate this approach. The result of using heuristics is slower scanning and system lag.

It is also important to note that not all AV software is created equal. Not every AV application will catch all known malware. VirusBulletin is an independent AV software testing laboratory. According to their results, commercial AV software is capable of detecting between about 60-98 percent of known malware.

Most of the major AV software developer results are clustered in the 95 percent range. Even with these, 95- percent detection means 1 in 20 known malware will go undetected by these applications. Of course, a zero-day--by