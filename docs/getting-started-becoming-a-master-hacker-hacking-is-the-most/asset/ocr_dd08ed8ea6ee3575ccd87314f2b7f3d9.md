![](bbox=[0.12, 0.09, 0.88, 0.45])

As you can see above, Wireshark has listed every IP address with activity and some basic statistics for each IP address.

Now that we understand the basics of using a packet analyzer like Wireshark, let’s apply it to a real-world problem —the NSA’s EternalBlue exploit that we used in Chapter 9 to exploit the Windows 7 system.

# ### Using Wireshark To Analyze the NSA’s EternalBlue Exploit

Throughout this book, we have been focusing on the notorious EternalBlue exploit that was stolen from the NSA, possibly by Russian hackers. In this section, we want to see what Eternal Blue looks like from a packet-level inspection in Wireshark. This analysis can help us to understand how EternalBlue works, which can lead to better security to prevent it (creating an anti-virus or IDS’s signature) and possibly the development of exploits similar to it.