# The Programmer's View of Linux

as Borland C++ and Borland Pascal. It understands C syntax, C++ syntax, and assembly syntax—though, alas, not the assembly syntax we'll be using. (On more on this sad disconnect later.) EMACS can build executable from inside the editor and do an awful lot of things I've never occasion to fool with. Whole books have been written on EMACS (O'Reilly has one) and would be worthwhile to grab such a book and digest it. If you intend to stick with Linux and any significant programming for it, EMACS is indispensable. Learn as much of it as you can.

# It's a C World

I'm a notorious Pascal bigot, and it pains me to say this, but Linux (as a genuine implementation of Unix) is inescapably a C world. Most of Linux is written in C, and what little isn't in C is in assembly. Virtually all the programming languages you'll see for Linux that don't involve interpreted languages as Perl or T will be in C. Most significantly (as I explain in greater detail later), the runtime library your assembly programs will use to communicate with the operating system is written in C and requires that you use the C protocols for function calling, rather than the more sensible Pascal ones.

So, before you attempt your first assembly program, buy a book and get down and hack some C. You don't need to do a lot of it, but make sure you understand all the basic C concepts, especially as they apply to function calls. I'll try to fill in the lower-level gaps in this book, but I can't teach the language itself nor all the baggage that comes with it. You may find it distasteful (as I did and do) or you may love it, but what you must understand is that you can't escape it, even if your interest in Linux is assembly language.

There are some excellent implementations for Linux, most of them free, so if you don't stick with assembly you have some alternatives to C. My choice is FreePascal 32. Go to the following Web site for more details and for the software itself: http://gd.tuwien.ac.at/languages/pascal/fpc/www/

# NASM for Linux

Another (minor) reason that I chose NASM as the focus assembler for this book is that a very good implementation—still free—exists for Linux. I've