# ## Summary

+   like **tcpdump**, **etheral** sniffs packets on the wire

+   unlike **tcpdump**, **etheral** has a GUI and lets you drill down into the detailed structure of each packet

+   just as with **tcpdump**, you can apply a capture filter to capture only the packets you are interested in

+   you can also apply a display filter to show only some of the packets you have captured. You can change or remove the display filter at any time to show a different set of packets, or all the packets you have captured.

+   you can use **etheral** to convert capture file formats, by reading in a file in one format and saving it as another

+   the **ngrep** packet sniffer is a quick way to display the contents of packets as ASCII text, and/or to select packets that match a given textual pattern. You specify patterns using regular expressions.

# ## What's next?

In the next chapter we look at the World Wide Web and its HTTP protocol.

# ## Notes and further reading

+   □ [http://www.etheral.com](http://www.etheral.com)

is the **etheral** Web site. It has a tutorial, as well as all the downloads. The **etheral** distribution includes the **editcap** (edit capture file) program, which lets you edit or convert capture files. However, an easier way to edit a capture file is to exclude packets you don't want using a display filter, and then tick the **Save only packets currently being displayed** option in the **Save as** dialog.

+   □ [http://www.packetfactory.net/Projects/ngrep/](http://www.packetfactory.net/Projects/ngrep/)

is the **ngrep** Web site. **ngrep** on Windows needs **packet.dll**, but if you've installed **Windump** (the Windows version of **tcpdump**) you'll have that already.

**ngrep** uses the same **libpcap** library as **tcpdump** and **etheral** to capture packets, which explains why the filter expressions are identical.

Regular expressions are used in many different programs on Linux and UNIX (and occasionally elsewhere, such as Microsoft's Operations Manager, MOM) for specifying search patterns, and search-and-replace operations. The expressions used in **ngrep** are the same as used in the Emacs programmable editor (which we used for almost all our UNIX-based work for this book). For a reference table giving the full regex syntax, which explains the use of the " ( ... ) " construct we used in the tip in Module 13.8, see Web Appendix 16.

+   □ [http://www.uit.co.uk/resources>ngrep regular expressions](http://www.uit.co.uk/resources>ngrep%20regular%20expressions)