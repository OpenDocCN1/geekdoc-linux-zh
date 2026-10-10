
- GPL software must be available in source form and may be used for arbitrary purposes.
- It is expressly allowed to modify the source and to distribute it in unmodified or modified form, as long as the receiver is given the same rights under the GPL.
- It is also expressly allowed to distribute (or even sell) GPL software in executable form. In this case, the source code (including the *GPL rights*) must be furnished alongside the executables, or must, during a certain period of time, be made available upon request.

“Source code” in this context means “everything necessary to get the software to run on a computer”. What that means in a particular case—for example, if it includes the cryptographic keys necessary to start a modified Linux kernel on an appropriately “locked-down” computer—is the subject of heated discussion.

If somebody buys GPL software for money, they naturally obtain the right not just to install that software on all their computers, but also to copy and resell it (under the GPL). One consequence of this is that it does not make a lot of sense to sell GPL software “per seat”, but one important side benefit is that prices for, e.g., Linux distributions stay reasonable.

- If you write a new program incorporating (parts of) a GPL program, the new program (a “derived work”) must also be placed under the GPL.

Here, too, there is heated debate as to how much and which parts of a GPL program must be incorporated into another program to make that program a “derived work”. According to the FSF, using a dynamically loadable GPL library within a program forces that program under the GPL, even if it does not by itself contain any GPL code and therefore cannot be considered a “derived work” in the legal sense. How much of this is wishful thinking and how much is actually legally tenable must, in principle, be determined in a court of law.

The GPL stipulates rules for modifying and distributing software, not its actual use.

Right now two versions of the GPL are in widespread use. The newer version 3 (also called “GPLv3”) was released at the end of June, 2007, and differs from the older version 2 (also “GPLv2”) by clarifications in areas such as software patents, the compatibility with other free licences, and the introduction of restrictions on trying to make changes to theoretically “free” software within devices impossible through special hardware (“tivoisation”, after a Linux-based digital PVR whose kernel cannot be modified or replaced). The GPLv3 allows its users to add further terms. The GPLv3 did not meet with universal approval within the community, hence many projects (most prominently, the Linux kernel) have deliberately stayed with the simpler GPLv2. In addition, many projects distribute their code under “the GPLv2 or any later version”, so you can decide which version of the GPL to follow when distributing or modifying such software.

It is considered good style among the developers of free software to make contributions to a project under the same licence that the project is already using, and most projects insist on this at least for code to be incorporated in the “official” version of the software. Some projects even insist on *copyright assignments*, where the author of code gives their rights to the project (or a suitable organisation). The advantage of this step is that copyright in the code rests solely with the project, and that copyright infringement—which only the copyright holder has legal standing to go after—is easier to address. A side effect that is either wanted or explicitly undesirable is that it becomes easier to change the licence for the whole project, which is also something only the copyright holder is allowed to do.

In the case of the Linux kernel project, which explicitly does not require copyright assignment, a licence change is difficult or impossible, since the code is a patchwork of contributions from more than a thousand authors. The issue was discussed during the introduction of the GPLv3, and the developers agreed that it would be a gigantic project to sort out the legal provenance of every single line of the Linux kernel source code and obtain its authors’ consent for a licence change. Some Linux developers would be adamantly opposed, while others cannot be located or may even be deceased, and the corresponding code would have to be replaced by something similar with a clear copyright. However, at least Linus Torvalds remains a supporter of the GPLv2, so the problem does not really arise in practice.

## GPL and money

The GPL does not stipulate anything concerning the possible price of the product. It is completely legal to give away copies of GPL software or to ask for money, as long as you furnish source code or make it available on request and as long as the receiver also gets the GPL rights. This means that GPL software is not necessarily “freeware”.

You can find out more by studying the GPL [GPL91], which must be distributed with each GPL-ed product (including Linux).

The GPL is considered the most consistent of free licences in the sense that—as we said—it tries to ensure that, once published under the GPL, code must *remain* free. On various occasions companies tried to incorporate GPL code into their own products that they were not about to release under the GPL. However, after being sternly reprimanded by (most often) the FSF as the copyright holder, these companies have come into compliance with the GPL. At least in Germany, the GPL has also been validated in court—a Linux kernel programmer could obtain judgement in the Frankfurt district court against D-Link (a manufacturer of networking components, in this case a Linux-based NAS device), which he had sued for not complying with the GPL when distributing their device [GPL-Urltd06].

Why does the GPL work? Some companies which considered the GPL restrictions onerous have tried to declare, or get it declared, invalid. For example, in the United States it was termed “un-American” or “unconstitutional”, and in Germany a company tried to use antitrust law to invalidate the GPL since it supposedly implied illegal price fixing. The idea seems to be that GPL software can be used by anyone for anything if something is demonstrably wrong with the GPL. All of these attacks ignore one important fact: Without the GPL, nobody except the original author would have the right to do anything with the code, since actions such as distributing or, in fact, selling the software are reserved by copyright law. So if the GPL disappears, all other parties interested in the code are a lot worse off than before.

A lawsuit where a software author sues a company that distributes his GPL code without complying with the GPL would approximately look like this:

**Judge** What seems to be the problem?

**Software Author** Your Lordship, the defendant has distributed my software without a licence.

**Judge** (to the defendant’s counsel) Is that so?

At this point the defendant can say “yes”, and the lawsuit is essentially over (except for the verdict). They can also say “no” but then it is up to them to justify why copyright law does not apply to them. This is an uncomfortable dilemma and the reason why few companies actually do this to themselves—most GPL disagreements are settled out of court.

If a manufacturer of proprietary software violates the GPL (e.g., by including a few hundred lines of source code from a GPL project in their product), this does not imply that all of that product’s code must now be released under the terms of the GPL. It only implies that they have distributed GPL code without a license. The manufacturer can solve this problem in various ways:

- They can remove the GPL code and replace it by their own code. The GPL then becomes irrelevant for their software.
- They can negotiate with the GPL code’s copyright holder (if available and willing to go along) and, for instance, agree to pay a license fee. See also the section on multiple licenses below.
- They can release their entire program under the GPL *voluntarily* and thereby comply with the GPL’s conditions (the most unlikely method).

Independently of this there may be damages payable for the prior violations. The copyright status of the proprietary software, however, is not affected in any way.

### 2.2.4 Other Licences

In addition to the GPL, other licences are popular in the context of FOSS. Here is a brief overview:

**BSD licence** The BSD licence originated with the University of California in Berkeley’s Unix distribution and is intentionally kept very simple: The recipient of the software is basically allowed to do with the software whatever they want as long as they do not create the impression that their use is endorsed by the university (or, by extension, the original software author). Any liability for the program is excluded as far as possible. The licence text must be preserved within the program’s source code and—if the program or modified versions are distributed in executable form—its documentation.

If a software package contained BSD-licenced code, the BSD licence used to require that any promotional material for the software or system in question mention this fact and the copyright holder. This “advertising clause” has since been dropped.

Unlike the GPL, the BSD licence does not try to keep the software’s source code public. Whoever obtains BSD-licenced software can essentially integrate it into their own software and distribute that in binary form (the GPL would require them to also distribute corresponding source code under the GPL).

Commercial software companies like Microsoft or Apple, who are generally less than enthusiastic about GPL software, usually have no issues with BSD-licenced software. Windows NT, for example, used to contain TCP/IP networking code from BSD (in adapted form), and large parts of the Macintosh’s OS X operating system kernel are derived from BSD.

Within the FOSS community, opinions have differed for a long time as to whether the GPL or the BSD licence is “more free”. On the one hand it makes sense to state that, as a recipient, one can do more with BSD-licenced software, and that therefore the BSD licence conveys more
