mechanisms which shuffle memory images to and from a slower storage medium such as disk.

The idea was somewhat slow in spreading to all systems, but almost all computers built today have some mechanism to permit or support virtual memory. (The exception is for processors used in embedded systems, i.e., those which have a specific control function which can reside entirely in main memory. Your microwave oven control is an example of such an embedded system.) In most cases, hardware support for virtual memory consists simply of a mechanism to stop and restart a “faulting” instruction. The details of moving memory images is left to specialized software. At the extreme, virtual memory support on the PRIME system was implemented entirely in firmware. We’ll take a detailed look at virtual memory in Section 5.4.

An aphorism for the computer age says “Virtual' means never knowing where your next byte is coming from.”

# ### 2.4.3 Filename Expansion In Command Lines

Unix systems have long possessed a feature called *globbing* as part of the command line processing. Globbing replaces special regular expression patterns with file names which match the patterns. Another term for this is “wild card substitution”.

The SDS-940, and later the Tenex operating system on the DECSystem-10s, added interactive file name expansion. This permitted the user to type part of a file name and then, by using a reserved character such as tab, have the system fill out the rest of the file name or produce a list of possible file names.

This new feature was first introduced to Unix users as a patch to the C shell, but it is now part of a number of shells found in Linux distribution kits.

# ### 2.4.4 Bit-Mapped Display

The Alto and Dorado systems were designed at Xerox PARC in 1974 to use a bit-mapped display for flexible user interaction[50, 29]. This spawned a number of successful follow-on projects such as the AT&T Bell Laboratories’ Blit and the Apple Lisa[39]. These in turn have