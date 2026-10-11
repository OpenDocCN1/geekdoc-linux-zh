
# About the Authors

## Will Hentzen

Will Hentzen fills the role of “player-coach” at Hentzenwerke Publishing, a 7-year-old, Milwaukee-based publisher that specializes in titles covering high-end software development and, more recently, the migration of Windows developers and users to Linux.

Will started out life as a custom software developer using dBASE II (he still has the original 8 1/2 × 11 gray binder of documentation, much to the chagrin of his wife), and switched to FoxPro in 1990. Besides billing 15,000 hours in the '90s, he presented more than 70 papers at conferences throughout North America and Europe, edited *FoxTalk*, Pinnacle Publishing’s high-end technical journal for seven years, and has hosted the Great Lakes Great Database Workshop since 1994. He was a Microsoft Most Valuable Professional from 1995 through 2003 for his contributions to the FoxPro development community, and received the first Microsoft Lifetime Achievement Award for Visual FoxPro in 2001.

Will began writing in order to develop credentials to bolster his software-development career. His first book, *Rapid Application Development with FoxPro*, showed up in 1993, and six more have appeared since. He started Hentzenwerke Publishing in 1996 to self-publish a specialized volume on software development, and then began producing Visual FoxPro books when the major publishers abandoned the market in 1998. Sensing the impending acceptance of Linux on the desktop and anticipating a demand for custom business applications on those Linux desktops, he turned his attentions to Linux in 2002, and will have eight narrowly targeted Linux and open-source books available by the end of 2004. HWP’s backlist now numbers more than 30, with some 60 authors and editors worldwide on the payroll.

Will has a B.S. in mechanical engineering from Rose-Hulman Institute of Technology and currently spends his copious amounts of spare time with his five kids and volunteering for the local school district. An avid distance runner, who logged nearly 50,000 lifetime miles and, pending recovery from a severe injury a few years ago, hopes for one more shot at a sub-15- minute, 5,000-meter clocking—before age and common sense close the door on that activity.

You can reach Will at will@hentzenwerke.com.

## Chris Herborsth

Chris Herborsth is an award-winning senior technical writer with more than 10 years of experience in the field of technology (http://www.pobox.com/~chris/chris-resume.html), with a background in operating systems, programming, and other interesting areas. When he's not playing with his son or hanging out with his wife, Chris spends his spare time designing and writing video games, enjoying various Nintendo GameCube titles, and fretting over how long it takes him to finish playing games on his PC. Chris can be reached at chris@pobox.com.

# How to Download the Files

**Hentzenwerke Publishing** generally provides two sets of files to accompany its books. The first is the source code referenced throughout the text. Note that some books do not have source code; in those cases, a placeholder file is provided in lieu of the source code in order to alert you of the fact. The second is the e-book version (or versions) of the book. Depending on the book, we provide e-books in either the compiled HTML Help (.CHM) format, Adobe Acrobat (.PDF) format, or both. Here’s how to get them.

Both the source code and e-book file(s) are available for download from the Hentzenwerke Web site. In order to obtain them, follow these instructions:

1. Point your Web browser to **www.hentzenwerke.com**.
2. Look for the link that says “Download.”
3. A page describing the download process will appear. This page has two sections:
   - **Section 1**: If you were issued a user name/password directly from Hentzenwerke Publishing, you can enter them into this page.
   - **Section 2**: If you did not receive a user name/password from Hentzenwerke Publishing, don’t worry! Just enter your e-mail alias and look for the question about your book. Note that you’ll need your physical book when you answer the question.
4. A page that lists the hyperlinks for the appropriate downloads will appear.

Note that the e-book file(s) are covered by the same copyright laws as the printed book. Reproduction and/or distribution of these files is against the law.

If you have questions or problems, the fastest way to get a response is to e-mail us at **books@hentzenwerke.com**.

# Introduction

When I first conceived of this book, Red Hat 6 had just shipped. I gave it a try, and found it not quite ready for desktop prime time—not ready for use by folks who just wanted it to run, who didn’t want to mess about with the internals just to get the machine running. It was approximately on a par with Windows 95—in some cases much easier, in others, still way too obscure. And then the early versions of OpenOffice.org showed up, and I realized that it was just a matter of time.

Not everyone saw it that way. At the time, people were saying that Linux would never make it on the desktop. I’d like to draw your attention to the word “never,” because these people were smart folks, but “never” is a really long time. The major reason they said “never”? Because there wasn’t an office suite like Microsoft Office available on the desktop.

Sure, there was KOffice, but it wasn’t file-format compatible with Microsoft Office. And there was OpenOffice.org, but in those early days, the first incarnations of Ooo led people to say “It’s unusable” in the same breath as “Linux will never make it on the desktop.” Six months later, they said that OpenOffice.org was pretty bad, but you could use it as an alternative to Microsoft Office if you were desperate. Six months after that, the regular line went “It’s usable in a small number of unique situations, but it’s not ready for use by the public.”

Seeing a trend here?

Another six months passed ... the OpenOffice.org team had kept the pressure on, continuing to add features and fix bugs, and suddenly it hit the radar—and people started deploying it on the desktop for real. Suddenly the story was “It’s just as good as Microsoft Office for the large majority of users.” And it’s immune to viruses, has significant, cost-saving features that Office doesn’t have, and can be downloaded and installed for free, without the risk of running afoul of licensing violations.

As I started this book, the realization that OpenOffice.org was for real hit Microsoft, and they started publishing materials to combat OpenOffice.org, treating it as a bona fide competitor, although they’d never admit it themselves. With OpenOffice.org, Linux was ready for the desktop.

While this isn’t supposed to be a testimonial for Ooo, the fact is that its availability has made Linux a contender on the desktop.

I switched my entire family to Linux last year, basically without telling them. One weekend my eldest daughter woke up to find that a SuSE box had replaced her Windows XP machine—and other than complaining about having to learn The GIMP for a couple of days, she’s never had a question. Web browsing, e-mail, word processing, spreadsheets and presentations for school projects, music, drawings—she does it all just as easily as with Windows. Our next two oldest kids share a Fedora Core box, on which they do most of the same things. And, again, they took to it without a second thought. Even my wife woke up one morning to a Red Hat 9 box, and except for an ancient sound card that didn’t work, she was back in business after a couple of hours of tweaking her settings to make them just the way she wanted them.

The best part of this transition is that they all interoperate with their friends and schoolmates transparently. Teachers don’t know that assignments are being done with OpenOffice.org or The GIMP, and friends don’t know that they’re exchanging e-mail and pictures with a Linux box. You might think my kids have an advantage, with a “local computer expert” available around the clock, but I actually spend less time helping them now. I don’t have to deal with blue screens, keeping service packs up to date, reinstalling the OS when the
