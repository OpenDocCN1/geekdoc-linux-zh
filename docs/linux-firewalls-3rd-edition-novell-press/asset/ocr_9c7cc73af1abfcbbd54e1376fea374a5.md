You have to make decisions that work in your environment. It may not make sense to deploy a computer outside of your firewall just for intrusion detection. All security is a trade-off between the assets you are trying to protect and the limited resources available to protect them.

# # Three Valuable Tools

An ever-growing number of tools and software exist to monitor network traffic. Some of these tools are free (as in price and speech) and some cost quite a bit of money. I’ve used both the expensive tools and the free ones, and I’m confident in saying that the free ones are better. The expensive tools are weak on functionality but strong on the pretty. The interfaces for many of the products provide a nice “look and feel” (though many of them seem to be somewhat unstable). In general, the open-source tools are a bit more involved to set up and use, but they provide better functionality and with a little work can produce some of the nicest looking graphs and other pictures that the expensive tools provide. For my money, I’d rather have intrusion detection tools that I could use quickly and easily when investigating a potential attack. Dealing with cumbersome, non-intuitive GUIs only gets in the way of the business of intrusion detection.

This section looks at a few monitoring tools with special emphasis on the tools that are covered later in the book.

# ## TCPDUMP

The primary tool in an intrusion detection analyst’s toolkit should be TCPDump. TCPDump places a network interface into promiscuous mode so that it captures every packet that arrives. Of course, this means that TCPDump needs to be run from the computer experiencing the possible intrusion or needs to be run from a computer that is the recipient of a “spanned” port in a switch environment. TCPDump is examined in greater detail in the next section.

# ## SNORT

Snort is one of the best intrusion detection systems available, free or otherwise. Snort captures network traffic in much the same way that TCPDump does. However, Snort uses a database of well-known attack signatures to provide a level of detection as well. Whereas TCPDump is more of a manual monitor, Snort is more automated insofar as the analyst doesn’t need to examine each packet. You can get more information on Snort at [http://www.snort.org/](http://www.snort.org/).

# ## ARPWATCH

ARPWatch is a tool used to monitor ARP traffic on a network. The goal would be for an administrator to spot possible ARP spoofing attempts as well as unknown devices that have entered the network. ARPWatch can be downloaded from [http://www-rrg.ebl.gov/](http://www-rrg.ebl.gov/). Like