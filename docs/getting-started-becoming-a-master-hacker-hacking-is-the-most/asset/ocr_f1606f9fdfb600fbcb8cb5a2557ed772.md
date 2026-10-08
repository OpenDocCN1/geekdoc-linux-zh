is the command

# **--deauth 100**

is the option to send 100 deauth frames into the AP

**-a <BSSID>** is the BSSID of the target AP

# **wlan0mon**

is your wi-fi adapter in monitor mode Now, when the client re-authenticates to the AP, airodump-ng will automatically detect the four-way handshake, capture it and write it to the file you designated (HackersAriseCrack).

When we do a long listing on our working directory, we will find five files creating by airodump-ng. The first one, Hackers-AriseCrack-1.cap contains the hash for cracking.

265 | Page

Now that you have the handshake, you simply need to use a hash cracking program such as hashcat to brute-force the password. Admittedly, this can be a slow and tedious process, making your selection of a good wordlist critical.

kali > hashcat -m 16800 HackersAriseCrack-01.cap /root/top10000passwords.txt If you are at first unsuccessful, go back to Chapter 8 and create a custom wordlist for the target using ceWL, or cup, or crunch, or all three. With this new custom wordlist, try once again to crack the hash with hashcat.

# **WPS**

Many people who buy and use Wi-Fi APs technically challenged. For them, setting up a Wi-Fi AP is a daunting