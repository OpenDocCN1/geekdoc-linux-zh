The tools that the Sockets API offers increase control of your program. You might use many of them in a single program so that you can predict the reliability of your program. Reliability in a network program is very elusive and requires several tricks, tips, and hints. The next chapter takes you to another level of reliability.

# Chapter 10. Designing Robust Linux Sockets

# IN THIS CHAPTER

+   - Using Conversion Tools
- Eyeing Return Values
- Capturing Signals
- Resource Management
- Critical Servers
- Client/Server Concurrency Issues
- Denial of Service Attacks
- Summary: Solid-as-a-Rock Servers

So, you want to write commercial-grade clients and servers. That’s a good goal—even if you might donate the work to Open Source. No one likes to be criticized for his code. So how do you make good code great? Good question.

You could consider what you’re trying to accomplish. If you are writing for a specific type of user, do you have one in mind? Can you work with him and get ideas about the possibilities? How reliable do the clients and servers need it to be?

Writing robust network programs is similar to regular programming, but you have to look at the big picture first; your program always runs at the same time as any connected program. That opens the picture quite wider. You have to consider more than just making the source readable.

This chapter provides several gems of advice on how to deal with these issues. It cannot be comprehensive; entire books are available just on writing solid code. But it can help you avoid the more typical network programming obstacles.

# Using Conversion Tools

The first step in creating good, robust socket programs is to use the Socket API’s conversion tools. You have a wealth of tools that convert the addresses, names, and binary numbers back and forth. This is important if you want to ensure portability, testability, and longevity of your code.

As described in [Chapter 2, "TCP/IP Network Language Fluency."](Chapter_2_TCP_IP_Network_Language_Fluency) the network uses the big endian binary storage format. You may have an alpha or 68040, which are themselves big endian as well. But, you probably want everyone in the Linux community to use your creative work. These tools automatically make the binary of the structures right. If you are on a big endian computer, you lose nothing—the libraries automatically map all conversion calls to do nothing, so your program does not spin its wheels in a useless call.

Thousands of programmers have tested all the libraries on your Linux machine. Some of these tests may admittedly be ad hoc. However, the GNU organization is very serious about the reliability of their packaged libraries. The thoroughness and almost nit-pickiness of these test procedures have made the libraries Linux uses solid. This foundation gives your program strength as well.