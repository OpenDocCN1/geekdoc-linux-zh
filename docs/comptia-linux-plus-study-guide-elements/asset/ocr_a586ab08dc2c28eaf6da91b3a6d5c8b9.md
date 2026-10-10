# # Physical Access Problems

The first broad category of security problem relates to physical access to the computer. In brief, if a miscreant has physical access to your computer, that person can do almost anything to it. Thus, controlling physical access to the computer is extremely important.

You may think of a system as secure because it has solid passwords and other protections. With a Linux emergency disk, though, somebody who gains physical access to your computer can boot into an environment that you don't control but that can still read and write all your important files, including sensitive files such as `/etc/shadow`. You can put up obstacles to easy access, such as using BIOS passwords. These require you to type a password before the computer boots at all. This protection can be overcome by resetting a jumper on the computer's motherboard, though, so a determined intruder can get around it. What's more, if data theft is the goal, the intruder can simply steal your hard disk, thus bypassing your BIOS password.

Very high-security installations may encrypt all the data on the hard disk to minimize the risk of data theft. This approach requires installing special software, such as loop-AES (`http://sourceforge.net/projects/loop-aes/`), dm-crypt (`http://www.saout.de/misc/dm-crypt/`), or True-Crypt (`http://www.truecrypt.org`).

Individual computers aren't the only elements for which physical access is a threat. Your local network infrastructure, if breached, can give intruders a way to access your local computers, bypassing the protections afforded by your router and firewall software. If you use a wired network exclusively, this risk is limited, but not nonexistent—somebody could break in or abuse access provided to visitors to plant a small computer on your network.

![](bbox=[0.18, 0.52, 0.22, 0.55])

# ## Real World Scenario

# ### Laptop Computer Security

Laptop computers present unusual security concerns. Such computers can be easily stolen, particularly if they're used in a portable manner rather than residing permanently in one secure room or building. If you use a laptop computer in a public space, it's also easy for other people to see what you're doing with it. Somebody who's up to no good might even be able to discern a password you type on a laptop in public, particularly if you type your password slowly.

You may want to consider using extreme measures, such as full-disk encryption, on laptop computers even when you wouldn't employ such tools on workstations or servers. At the very least, you should probably use different passwords on your laptops than on your workstations and servers.

The security picture for laptops isn't entirely bleak, though. Cases are occasionally reported of thieves being caught because of laptop features. For instance, one burglar (reported in `http://perens.com/works/articles/Burglar/`) was caught when he used a stolen laptop's camera to take photos of himself that were subsequently uploaded by an automatic backup utility to off-site storage maintained by the laptop's true owner!