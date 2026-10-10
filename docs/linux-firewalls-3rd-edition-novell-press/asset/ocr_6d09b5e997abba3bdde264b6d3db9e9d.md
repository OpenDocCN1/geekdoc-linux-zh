is equivalent to this:

greater  1500

# ## Beyond the Basics with TCDump

You should now have a feel for the basic syntax of TCDump, including some of the options, the syntax, and TCDump expressions. The amount of troubleshooting and diagnostics that can be accomplished with even a basic grasp of TCDump syntax makes it an essential tool for anyone managing networked computers. However, even a basic knowledge of TCDump is sometimes insufficient to examine some problems successfully. To examine more difficult problems, you may find that you need to go beyond the basics of TCDump.

Going beyond the basics of TCDump requires deeper understanding of the protocols themselves. Knowing the flags of TCP or the types of ICMP can help to narrow the focus to only the packets of interest. Although this information and knowing how to use it with TCDump is not mandatory, having the ability to call on the information at any time is valuable to say the least. Take time to familiarize yourself with TCDump’s more involved syntax. It costs nothing but time to test a packet-filtering expression to see how it works under various net-work conditions.

# ## Using TCDump to Capture Specific Protocols

In this section, I’ll give some examples that show you how to capture various forms of net-work traffic for monitoring purposes. Included among the examples, you’ll see what a DNS query looks like through TCDump, some ICMP (ping) examples, and various TCP- and UDP-based protocols. After you see how normal traffic looks, I’ll then show you some of the fun stuff. Specifically, I’ll show what some types of attacks look like through TCDump so that you might be able to quickly detect these when coming into (or out of) your network.

Throughout this section, I’ll be using a few different programs to generate traffic for TCDump to capture. My primary tool for TCP-related captures will be telnet. I’ll use telnet to generate traffic and mirror what the real protocol (or close to it) does in the real world. Generation of DNS queries will be accomplished using both the dig command and the host command. The ping and tracertoute commands will be used. Finally, the hping2 command will be used to generate ICMP traffic as well as other interesting packets, especially in the attack section. With the exception of hping2, all of these programs are installed on most major Linux distributions.