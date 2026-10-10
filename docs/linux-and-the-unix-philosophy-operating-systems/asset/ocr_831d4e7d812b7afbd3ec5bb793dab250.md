I/O bandwidth becomes an issue. Consequentially, computer hardware vendors love CUIs.

# **6.1.4 Programs with CUIs are hard to combine with other programs**

One strength of Unix is the way its programs interact with each other so effectively. Programs with CUIs, because they assume that the user is human, do not interface well with other programs. Software designed for communicating with other software is usually much more flexible than the software designed to communicate with people.

Do you remember the example of workers loading a moving van? We said that the large pieces did not fit well with each other and it was the small pieces that provided the most flexibility. Simiarly, programmers find it difficult to connect programs having CUIs to each other because of their size. CUIs tend to result in huge programs. Large programs, like large pieces of furniture, are not very portable. Movers don’t say, “Hand me that piano, will ya?” any more than programmers move complex, monolithic applications from one platform to another overnight.

CUI programs’ inability to combine with other programs causes them to grow to massive proportions. Since the programmer cannot rely on interfacing easily with other programs on the system to obtain the required capabilities, he must build new features into the program itself. This deadly spiral feeds on itself: The more features built into the CUI program, the larger it becomes. The larger it becomes, the greater the difficulty in interfacing it with other programs. As it gets harder to interface with other programs, the CUI program itself must incorporate more features.

# **6.1.5 CUIs do not scale well**

CUIs tend to work well when dealing with only a few instances. By limiting choices, they can make it easier for an inexperienced user to accomplish complex tasks. As long as there are not too many instances, the user is usually content to respond to the prompts. The number of prompts can become unwieldy, however, when one must respond to several hundred of them.

A popular program (a shell script, really) provided by many Unix system vendors is adduser. It allows the system administrator to add a new user account to the system via a “user-friendly” CUI. Most of the time it works well. The problem with adduser becomes evident when you must add, say, several thousand users at once.

Once a university had decided to change from another OS to Unix. Several thousand user accounts were to be transferred to the new system. It didn’t take long for the system administrators to realize that running adduser that many times wasn’t going to cut it. They ultimately settled on a solution that involved moving the user account files from the old system to the Unix system. Then they wrote a shell script to convert them into files resembling the Unix password file. The irony was that the shell script written to do the conversion was shorter than adduser.

# **6.1.6 Most important, CUIs do not take advantage of software leverage**

Because CUI programs expect to communicate with a human being at some point, it is very