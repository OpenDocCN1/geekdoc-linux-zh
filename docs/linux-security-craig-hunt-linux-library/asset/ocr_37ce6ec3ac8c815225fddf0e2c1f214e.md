# ## In Sum

Security is a process, and putting up a strong defense is virtually useless unless you're willing to monitor your system for intrusions and stay vigilant. The `syslog` facility is a powerful system security tool, especially when the resulting log files are periodically monitored for abnormal behavior. This chapter describes two such tools: `swatch` and `logcheck`.

The value of examining log files, however, is greatly diminished if you can't be sure that their contents haven't been modified by an intruder in order to cover his/her tracks. Part of your security-monitoring procedures should include an integrity check on both log files and important system executables. This serves to assure you that the log files haven't been tampered with and that the executables haven't been replaced by Trojan horse versions.

Finally, it's easy to underestimate the importance of using good passwords that can stand up to naive intrusion attempts. Among the password-auditing tools currently available for Linux, John the Ripper stands out as a clear winner because of its performance and its ease of use.

Once you have implemented your system security measures and established procedures for system monitoring and auditing, it's time to consider your network layer defense. The next part of this book, Part 2, "Network Security," describes the server configuration issues that impact network security and introduces monitoring and auditing tools and procedures that apply to the network layer.