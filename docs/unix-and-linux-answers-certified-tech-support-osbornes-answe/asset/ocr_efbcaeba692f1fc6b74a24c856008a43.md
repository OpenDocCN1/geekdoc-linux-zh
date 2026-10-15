generally does a much better job at it than NT. Microsoft never could manage print spooling well.

# SHELL EMULATIONS: MAKING NT FEEL LIKE UNIX, AND UNIX FEEL LIKE NT

# What is the "standard" UNIX shell?

There is no standard UNIX shell. The most common alternatives are the Korn shell (our personal favorite), the Posix shell (the default shell on most new UNIX versions, and a close relative to the Korn shell), the Bourne shell (generally the lowest common denominator), and the C shell. There are also alternative freeware shells, such as the Bourne Again Shell (bash), that have gained a lot of adherents since they're generally available on a wide variety of platforms including Linux. Versions of most of the available shells are available on whatever UNIX you find yourself working on, and you should choose the shell you use based on the needs of the environment you're in, or the amount of scripting you expect to have to do. Interactive users tend to find the C shell or the Korn shell the most comfortable alternatives, while intense scripting should be done on the Bourne, Posix, or Korn shell, but should generally be written to Bourne shell limitations to prevent cross-platform problems.

# How can I make NT behave like UNIX?

There are a couple of products on the market that let you mimic the rich command-line power of UNIX even on Windows NT. Probably the most prevalent is the MKS ToolKit from Mortice-Kerns (http://www.mks.com). If you spend your time jumping back and forth between UNIX and Windows NT or Windows 95, we highly recommend this package. It's not perfect and it has a couple of things we really, really wish it did better. Still, it's a remarkably good Posix or Korn shell emulation running on Windows NT, and it includes all the most common UNIX command-line utilities that we'd be lost without. It even includes a quite