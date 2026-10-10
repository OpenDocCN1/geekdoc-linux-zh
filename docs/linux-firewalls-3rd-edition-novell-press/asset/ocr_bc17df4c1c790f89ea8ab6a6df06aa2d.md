the files in question. For example, if files such as `/etc/resolv.conf` or even `/etc/shadow` change with no apparent reason, the administrator can take action.

Two popular filesystem integrity tools are Tripwire and AIDE. Tripwire had been the choice among administrators for a long time. However, Tripwire's license changes, thus making commercial uses of the software questionable and even making the open-source nature of the software questionable. AIDE was developed as an alternative. In the meantime, the Tripwire license changed back, so as of this writing Tripwire is again a traditional open-source package. However, I'm not going to cover Tripwire in this book due to the license changes. I don't want to have the license change yet again between the time I write this and the time you read it.

AIDE is covered in detail, and a more complete description of how filesystem integrity works is given, in Chapter 12, "Filesystem Integrity."

# # Log Monitoring

Monitoring log files is used to watch for anomalies that might indicate an attack. Although this method is used successfully, it can result in huge amounts of data and become cumbersome on large networks.

When combined with other tools, log monitoring can be made to work. For example, using log monitoring on a few key systems can reduce the amount of data being received. However, this and other such measures are really stop-gap measures because they do little to ensure the security of the systems that aren't monitored.

Numerous packages are available to monitor log files. Three such packages include Logsnorter, Swatch, and Logcheck. More information on each can be found at their respective websites or from within your system's documentation if the distribution includes them as available packages. I'll briefly cover Swatch here just to give you a taste of some of the capabilities of these types of tools.

# ## Swatch

Swatch is available with many Linux distributions as an add-on package or can be downloaded from `http://swatch.sourceforge.net/`. Swatch is highly configurable and can perform a number of actions based on a match.

Swatch works in several modes, including a mode called single-pass, which has the program parse a log file once, searching for matches and taking action based on those matches. Another mode sees Swatch perform a running `tail (tail1 -f)` of a log file looking for matches. By default, Swatch monitors `/var/log/messages` but it can be configured to monitor any file or even a socket.