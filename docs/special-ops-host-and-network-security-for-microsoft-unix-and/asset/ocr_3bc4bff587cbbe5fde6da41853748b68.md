# Securing Exchange and Outlook Web Access • Chapter 7

someone might use an EXE file or a script embedded in an HTML message to propagate a virus does not make a rocket scientist. But who would have dreamed that someone would embed an e-mail virus in SCR file?

For this reason, viruses continued to sneak by the most savvy e-mail administrators well into 2001 and 2002. And for this reason, continued vigilance and even what may seem to be extreme restrictions on the e-mail system must be maintained.

> WARNING
> No anti-virus solution will be effective if its signatures and scanning engine are out of date. The software should be configured to check for virus signature updates at least once per day. And the minute you hear of a new e-mail-based virus, force a signature update immediately to see if new signatures have been released. If not, check again in an hour or two.

# Choosing the Correct Anti-Virus Solution

The first step toward a virus-free utopia is to make sure you have chosen the correct anti-virus software to work on the Exchange 2000 server. This software must be Microsoft Anti-Virus API (AVAPI) 2.0-aware. Most major anti-virus vendors on the market today provide AVAPI 2.0-aware solutions for Microsoft Exchange. But you must make absolutely sure that the product is designed to work with and on the Exchange server.

> WARNING
> Should you use a file-based scanner on the Exchange 2000 server? File-based scanners can cause dreadful (and fatal) problems for Exchange server due to the fact that these scanners may actually find a virus in an Exchange log or database file and remove the virus. Since file-based scanners (such as Norton Anti-Virus Corporate Edition) do not have a clue about ESE database checksums, they will corrupt the file. I have configured both Norton Anti-Virus for Microsoft Exchange and Norton Anti-Virus Corporate Edition on the same machine, but you must configure the file-based scanner to ignore the Exchange data, log file, and queue directories.

![](bbox=[0.708, 0.943, 0.928, 0.966])