to justify why copyright law does not apply to them. This is an uncomfortable dilemma and the reason why few companies actually do this to themselves—most GPL disagreements are settled out of court.

If a manufacturer of proprietary software violates the GPL (e. g., by including a few hundredes of lines of source code from a GPL project in their product), this does not imply that all of that product’s code must now be released under the terms of the GPL. It only implies that they have distributed GPL code without a license. The manufacturer can solve this problem in various ways:

+   * They can remove the GPL code and replace it by their own code. The GPL then becomes irrelevant for their software.
+   * They can negotiate with the GPL code’s copyright holder (if available and willing to go along) and, for instance, agree to pay a license fee. See also the section on multiple licenses below.
+   * They can release their entire program under the GPL *voluntarily* and thereby comply with the GPL’s conditions (the most unlikely method).

Independently of this there may be damages payable for the prior violations. The copyright status of the proprietary software, however, is not affected in any way.

# ## 2.2.4 Other Licences

In addition to the GPL, other licences are popular in the context of FOSS. Here is a brief overview:

**BSD licence** The BSD licence originated with the University of California in Berkeley’s Unix distribution and is intentionally kept very simple: The recipient of the software is basically allowed to do with the software whatever they want as long as they do not create the impression that their use is endorsed by the university (or, by extension, the original software author). Any liability for the program is excluded as far as possible. The licence text must be preserved within the program’s source code and—if the program or modified versions are distributed in executable form—its documentation.

If a software package contained BSD-licenced code, the BSD licence used to require that any promotional material for the software or system in question mention this fact and the copyright holder. This “advertising clause” has since been dropped.

Unlike the GPL, the BSD licence does not try to keep the software’s source code public. Whoever obtains BSD-licenced software can essentially integrate it into their own software and distribute that in binary form (the GPL would require them to also distribute corresponding source code under the GPL).

Commercial software companies like Microsoft or Apple, who are generally less than enthusiastic about GPL software, usually have no issues with BSD-licenced software. Windows NT, for example, used to contain TCP/IP networking code from BSD (in adapted form), and large parts of the Macintosh’s OS X operating system kernel are derived from BSD.

Within the FOSS community, opinions have differed for a long time as to whether the GPL or the BSD licence is “more free”. On the one hand it makes sense to state that, as a recipient, one can do more with BSD-licenced software, and that therefore the BSD licence conveys more