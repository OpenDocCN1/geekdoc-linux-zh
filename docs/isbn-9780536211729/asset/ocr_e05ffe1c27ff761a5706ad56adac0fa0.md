+   - "Firewalls and the Corporate Moat" on page 67
- "Turn Off Unneeded Services" on page 80
- "High Security Requires Minimum Services" on page 87
- "Replace These Weak Doors with Brick" on page 88
- "New Lamps for Old" on page 97
- "United We Fall, Divided We Stand" on page 109

# 2.1 Understanding Linux Security

![](bbox=[0.105, 0.31, 0.894, 0.4])

Some of the ideas behind Linux security are covered in this chapter, each as well as innovative new perspectives for viewing security. New ways will be considered to avoid the single "wall" of security that permits a single crack in that wall to void all security. Linux is based on the UNIX security model. This model was designed by some of the top Ph.D. computer scientists in the U.S. It has undergone 30 years of analysis, development, and evolution by everyone from noted scholars to crackers to Department of Defense and other government security experts. It has stood the test of time.

# 2.1.1 You Are in a Maze of Twisty Little Passages

A Linux system is a maze of twisty little passages, each with unknown connections and doors with locks of different strengths. The path to cracking a system may be long and twisty with many dead ends. This maze is shown in Figure 2.1.

As you can see in Figure 2.1, a cracker need find only one of many possible paths from the Internet to "owning" a system's root account or important database. The particular rooms offering unexpected (paths) in Figure 2.1 are, if any of them are broken into, the most frequent ways that Linux systems exist on your systems, you will want to read the appropriate sections of the book to ensure that the unexpected passages are blocked. These most severe vulnerabilities are also listed in Table 2.1. These problems and their solutions are discussed.

As you can see in Table 2.1, the most frequent avenues for breaking into a Linux box are common features in many sites. You can also see that many of the avenues are buggy system software or applications rather than a simple "misconfiguration" by the SysAdmin. This means that proper configuration of the system is not enough. You also need to be subscribed to the appropriate security mailing lists and work with your users and programmers to achieve a secure system. Following realistic example shows how a cracker might search for your system's vulnerabilities and take advantage of them to break in.