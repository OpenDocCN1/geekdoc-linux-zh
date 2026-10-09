This command should be added to your /etc/rc.shutdown script to ensure a clean termination of the auditing process. Auditing can be paused and restarted by specifying off and on as arguments to the audit command.

# ADDITIONAL SECURITY TOOLS

A tremendous number of open source and free software tools are available for AIX. These tools can help secure your systems and ensure the integrity of the data stored within. Several of the more popular tools are listed in the following sections.

Note that while many of the tools listed are available in a compiled, ready-to-install format, it is a good policy to build programs from the source when possible.

# John the Ripper

One of the most important things that you can do to protect your systems is to help your users develop good password habits. Users may not want this help, but it is critical that they understand the need for it and for the creation of strong passwords to protect their accounts.

John the Ripper is a password-cracking tool. It takes as its input a list of encrypted passwords and tries to determine their unencrypted values. If John the Ripper can determine a user’s password, that password is probably not very strong.

The homepage for John the Ripper is http://www.openwall.com/john/. The latest release of John can be downloaded in source form from that site, or in a compiled LPP format from http://www.build.de/pub/.

# Swatch

Swatch, “The Simple WATCHer,” is a Perl application that continually monitors log files, looking for patterns defined in a configuration file. When the pattern is detected, swatch can perform a number of actions, such as executing a program or e-mailing the detected error to a specified address. Swatch automates the tedious process of constantly reading log files, separating the important entries from the noise.

Swatch can be downloaded from http://eta.cs.colorado.edu/~swatch/. It requires Perl, which is included with AIX 5L.

# Tripwire

Tripwire is a file integrity monitoring tool, available both free and in a commercial version. Along with the features provided by the TCB, Tripwire offers a number of additional features and reporting capabilities. It is also available for a wide variety of platforms, and is thus an excellent solution for heterogeneous data centers. The commercial version provides centralized configuration, monitoring, and reporting. For more information about Tripwire, see http://www.tripwire.com/. Instructions for building the free version of Tripwire on AIX can be found at the IBM eServer