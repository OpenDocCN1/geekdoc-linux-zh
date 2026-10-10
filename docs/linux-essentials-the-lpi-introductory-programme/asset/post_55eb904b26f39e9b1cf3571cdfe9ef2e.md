
This means that it is, in principle, illegal to copy a program or a complete software package without the explicit consent of the copyright holder (the programmer or their employer).

![](img/44bdd771e9c9b1353d2401c2892b2459_29_0.png)

In the early days of the computer it was not common for software to be sold. You were either given it together with your computer (which used to be expensive enough—millions of dollars) or would write it yourself. On the university scene in the 1960s and 1970s it was utterly normal to swap or copy programs, and in 1976 a certain Bill Gates was horrified to find out that his BASIC interpreter for the MITS Altair 8800 proved very popular indeed and he got lots of kudos for it, but almost nobody found it necessary to pay his asking price! Of course that wasn't proper on the users' part, but even the *idea* that software should be paid for was so outlandish at the time that few people actually entertained the thought.

![](img/44bdd771e9c9b1353d2401c2892b2459_29_1.png)

As computers spread through offices during the late 1970s and 1980s, it became more and more common to sell software instead of giving it away. Not only that—the software companies sold only the executable machine code, not the source code that people would be able to examine to find out how the software worked, or even to modify. At some point, Richard M. Stallman, who used to be an MIT researcher, decided to try and reverse this trend by working on a system that would emphasise the culture of sharing that was the norm during the 1960s and 1970s. This “GNU” system³ remains unfinished, but many of its components are now in use on Linux systems.

Richard M. Stallman (often called “RMS” for short) can be thought of as the father of the idea of *free software*. In this context “free” does not mean “free of charge”, but that the user is “free” to do various things they would not be able or allowed to do with proprietary software⁴. RMS calls a software package “free” if four conditions, the “Four Freedoms”, are met:

- The freedom to run the program for any purpose (Freedom 0).
- The freedom to study how the program works, and change it to make it do what you wish (Freedom 1).
- The freedom to redistribute copies so you can help your neighbor (Freedom 2).
- The freedom to improve the program, and release your improvements (and modified versions in general) to the public, so that the whole community benefits (Freedom 3).

Access to the program's source code is a prerequisite for freedoms 1 and 3. The idea of free software was favourably received in general, but even so the goals of RMS and the *Free Software Foundation* (FSF) were often misunderstood. In particular, companies took exception to the word “free”, which in spite of appropriate clarifications was often confused with “cost-free”. At the end of the 1990s, Eric S. Raymond, Bruce Perens and Tim O’Reilly created the *Open Source Initiative* (OSI), whose goal it was to provide better and less ideological marketing for free software. The FSF wasn't enthusiastic about this “watering down” of its ideas, and in spite of the very similar goals of the FSF and OSI the controversy has not died down completely even now (which to a certain degree may be due to the considerable egos of some of the main people involved).

![](img/44bdd771e9c9b1353d2401c2892b2459_29_2.png)

While the “free” in “free software” encourages the confusion with “no charge”, the “open source” in “open-source software” can be interpreted such that the source code may be inspected but not modified or passed on—both of which are basic tenets of the OSI. In this sense, neither of the terms is 100% unambiguous. The community often refers to “FOSS” (for free and open-source software) or even “FLOSS” (free, libre, and open-source software, FLOSS where the libre is supposed to support the sense of “liberty”).

How to make money with free software if anyone is allowed to change and copy the software? A very legitimate question. Here are a few ideas for “open-source business models”:

- You could provide additional services such as support, documentation, or training for free software and get paid for that (this works very well for your author’s company, Linup Front GmbH, and the LPI seems to be able to make a living from selling Linux certification).
- You could create bespoke improvements or extensions for specific customers and be paid for your time (even if the result of your development then becomes part of the generally available version. This works even for free software that you didn’t originally write yourself.
- If you distribute a software package, you could provide a basic version as FOSS and hope that this will entice enough people to buy the proprietary “full version” to really get things done. (The jargon expression for this is “open core”.)

This is a two-edged sword: On the one hand, it is of course nice if there is more free software, but on the other hand the result is often that you need the proprietary version because important functionality is not available in the free version and it would be too much work to add that functionality independently. In this case, the “free” version mostly serves as a PR engine if the manufacturer wants to appear modern and “open-source friendly”—to “talk the talk” without “walking the walk”.

### 2.2.2 Licences

How does a piece of software become “free” or “open source”? We mentioned that certain rights—for example, the right to copy or modify a work—are reserved for the author of the work, but that these rights can also be passed on to others. This happens (if it happens) by way of a “licence”, a legal document which specifies the rights that the receiver of the software obtains by buying, downloading, … it. Copyright as such allows the buyer (or lawful downloader) of a software package to install that software on a computer and to start and run it. This results simply from the fact that the software was made available to them by the author—there is evidently no point in selling somebody a program that the buyer isn’t allowed to use¹. (Conversely, whoever gave the author money for the program has a right to use the program in exchange for their payment.) Other actions such as uncontrolled copying and distribution, or modifying the program, are explicitly forbidden by copyright, and if the original author wants people to be allowed to do these things they must be written into the licence.

Proprietary programs often come with an "end-user licence agreement" (EULA) that the buyer must accept before actually being able to use the software. The software vendor uses the EULA to forbid the buyer to do things the buyer would in fact be allowed to do by copyright law—such as selling the software "used" to someone else, or to say bad things (or indeed anything at all) about the software in public. Such an EULA is a contract that needs to be accepted by both sides, and the legal hurdles (at least in Germany) are fairly high. For example, a software buyer must be able to inspect the EULA conditions before buying the software, or it must at least be possible to return the software unused for a full refund if the buyer does not agree with the EULA.

On the other hand, the open-source licences for FLOSS are used to let the receiver of the software perform actions that would otherwise be forbidden by copyright. They generally do not try to restrict use of the software, but for the most part govern questions of modifying and distributing the software. In that sense they do not leave the software receiver worse off than they would have to expect from the sale of any other good. Hence, unlike EULAs, free-software licenses are usually not contracts that the receiver must explicitly accept, but one-sided declarations on the part of the software author, and the rights conferred by them constitute extra benefits on top of the simple usage rights inherent in the law.

By now there is a whole zoo of licences fulfilling the basic requirements for free or open-source software. The best-known free-software licence is the General Public License (GPL) promulgated by Richard M. Stallman, but there are several others. The OSI “certifies” licences that according to its opinion embody the spirit of open source, just as the FSF approves licences that safeguard the “four freedoms”. Lists of approved licences are available from those organisations’ web pages.

If you consider starting a free or open-source software project, you are certainly free to come up with your own licence fulfilling the requirements of the FSF or OSI. However, it is usually better to adopt an existing licence that has already been approved. This means that you do not need to obtain approval for your licence from the FSF or OSI, and the existing licences have usually been examined by legal professionals and can be considered reasonably water-tight—as an amateur in contract or intellectual property law you might overlook important details that could get you in trouble later on.

It is important to observe that the proponents of free or open-source software in no way intend to completely abolish copyright for software. In fact, free software as we know it can only work because copyright gives software authors the legal right to make the modification and distribution of their software contingent upon conditions such that the receiver of the software must also be given the right to modify and distribute it. Without copyright, everybody could help themselves to any available piece of software, and central tenets such as the “four freedoms” would be endangered because it would be possible for people to hoard without any sharing at all.

### 2.2.3 The GPL

The Linux kernel and large parts of what one would otherwise consider “Linux” is distributed under the General Public License (GPL). The GPL was developed by RMS for the GNU project and is supposed to ensure that software that was originally distributed under the GPL remains under the GPL (this type of licence is also referred to as a copyleft licence). This works approximately like this:

> 5 In fact, the copyright laws of many countries contain explicit clarifications stating that the process of copying a program from disk into RAM in order to run it on the computer is not subject to copyright.

³“GNU” is a “recursive acronym” for “GNU's Not Unix”.
⁴The “Free Software Foundation”, Stallman's organisation, calls this “free as in speech, not as in beer”.
