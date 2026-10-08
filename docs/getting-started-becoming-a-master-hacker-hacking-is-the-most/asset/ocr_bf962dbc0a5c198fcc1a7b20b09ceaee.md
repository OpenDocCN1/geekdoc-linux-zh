Metasploit does not help you hack with new, zero-day (never seen before) exploits, but instead catalogs and deploys tools and exploits against known vulnerabilities in operating systems, services, and applications.

It’s important to note that systems are NOT always patched and up-to-date. As we saw in the History of Hacking section in Chapter 1, even after the patch for the EternalBlue exploit was released, the attackers 31 | P a g e were able to exploit hundreds of thousands of systems around the world and garnar billions of dollars in ransom.

In this book, we will focus on the use of Metasploit and some Python scripts for exploitation.

# ## Post-Exploitation

Post-exploitation is what happens after the hack, or exploitation. The hack gets the attacker inside the system, but access is generally just the beginning. Post-exploitation can include grabbing passwords, accessing the database, turning on and accessing the microphone or webcam, etc. It may also include pivoting to compromise other parts of the network. For instance, if the hacker can compromise a single user on the network, that user’s systems will not likely have the valuable assets the hacker is seeking, such as the database that contains personally identifiable information, credit card numbers, or confidential information. The hacker needs to learn to pivot from the compromised system to other systems on the network to be successful.

# ## Covering Tracks

Once the exploitation is complete, and the post-exploitation havoc has been done (taking or reading documents, turning on the microphone, pivoting to other systems, etc.), the