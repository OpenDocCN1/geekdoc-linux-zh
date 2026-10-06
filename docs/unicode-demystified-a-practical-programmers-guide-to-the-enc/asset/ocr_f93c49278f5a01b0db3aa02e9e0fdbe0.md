# 370 Chapter 9 Networking and the Internet

With eight sets of hexadecimal groupings, you have 65,536⁸ = 2¹¹⁶ possible addresses. In an IPv6 address on a host with the default autoconfiguration, the first characters in the address are always fe80. The last 64 bits hold an interface ID which is often the MAC address (page 1478) of the Ethernet controller on the system.

# Communicate over a Network

Many commands that you can use to communicate with other users on a single computer system have been extended to work over a network. Three examples of extended utilities, all of which were introduced in Chapter 3, are electronic programs (such as ping), information-gathering utilities (such as finger), and communications (such as talk). These utilities are examples of the UNIX philosophy: Instead of creating a new, special-purpose tool, modifying an existing one.
Many understand a convention for the format of network addresses: user@(spoken as at host). When you use an @ sign in an argument to one of these utilities, the utility interprets the text that follows as a remote host. When it does not include an @ sign, the utility assumes that you are requesting information from or corresponding with someone on your LAN.
The prompts shown in the examples in this chapter include the hostname of the machine you are using. When you frequently use more than one system over a network, you may find it difficult to keep track of which system you are using at any particular moment. If you set your prompt to include the hostname of the current system, it will always be clear which system you are using. To identify the system you are using, run hostname or username -n:

```
$ hostname
kudos
```

See 579 and 749 for information on how you can change your prompt.

# finger: Displays Information about Remote Users

The finger utility displays information about one or more users on a system. The finger utility was designed for local use, but when networks became popular, it was obvious that finger should be enhanced to reach out and collect information remotely. In the following examples, finger displays information about all the users logged in the system named bravo: