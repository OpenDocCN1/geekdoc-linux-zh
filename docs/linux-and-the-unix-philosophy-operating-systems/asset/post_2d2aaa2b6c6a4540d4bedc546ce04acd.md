
## Chapter 4: The Portability Priority

### Overview

So there I was, an attendee at the 1991 USENIX Technical Conference, strolling the halls of Nashville's Opryland Hotel, reveling in the grandiose luxury of that country music citadel, picking my way through the crowds, hoping to happen upon someone famous, and basking in the satisfaction of having just signed a publishing contract.

Things had gone extremely well. My proposal for a book on the Unix philosophy was accepted without hesitation. ("So many people need to read this book.") Contract negotiations went smoothly. ("I'd like $n$ dollars for an advance." "Okay, you've got it.") A reasonable deadline had been set. ("We'll give you an extra couple of months to make it easier on you.") You couldn't have asked for a better situation.

To tell the truth, I was scared to death. After getting over the initial enthusiasm of signing up to author a book on a topic I'd been harping on for years, I ran headlong into a reality that I was mentally unprepared for: I now had to write the darn thing.

My past writing experience consisted of pumping out features for a regional entertainment magazine. I'd learned how to string words together. I knew about topic sentences, action verbs, and the use of passive voice. I could hook a reader and keep him interested. However, writing magazine articles only made me a great sprinter. Now it was time to run the marathon.

The first thing I did was sprint to a friend for advice. An author of several books, he had run this race before. What could I do, I asked, to get a handle on this seemingly insurmountable task?

"Buy a notebook PC," he replied.

Seeing the Neanderthal look on my face, he explained that writing a book is an all-or-nothing proposition. It takes an intense, concentrated effort to put so many thoughts down on paper. You must think about the book nearly always: while brushing your teeth in the morning, while driving to and from work, between meetings, while having lunch, during your workout at the health club, while watching television with the family, and before you go to sleep at night. The notebook PC is the only text entry device at once powerful and portable enough to enable you to write a book just about anywhere.

An amazing feat of modern microtechnology, the typical notebook PC puts most capabilities of a desktop PC in a package thinner than a three-ring binder. Weighing less than five pounds, its low-profile design makes it as easy to carry around as a college textbook. They come with hard disk drives and built-in modems, making them viable workhorses for everyday computing tasks such as calculating spreadsheets, word processing, and programming.

Some years ago, Apple Computer ran a television ad showing two executives discussing the merits of various personal computers. Both men were talking about technical specifications, and one appeared to have a profound revelation: The most powerful computer is not the one with the fastest CPU, the biggest disk drives, or the most teraflops. It is the one that is used most.

Judged solely by this criterion, the notebook PC will someday rank as the most powerful computer ever built. It doesn't have the blinding speed of, say, a laboratory supercomputer. Nor does it have the storage capacity of the latest disk farm technology. Its graphics capabilities will probably always lag behind the raciest desktop screens. Hardly the epitome of performance, it has only one real advantage: portability.

This brings us to the next tenet of the Unix philosophy. You might wish to make a special note of this one. It marks the reason Unix has nullified the longevity of thousands of man-years' worth of software development effort.

### 4.1 Tenet 4: Choose portability over efficiency

Software development involves choices, each of which represents a compromise. Sometimes the developer must write a short, simple subroutine because he doesn't have time to include a more sophisticated one. At other times a limited amount of RAM might be a constraint. In some situations one must avoid tying up a network connection with too many small data packets, because the network protocol in use favors transfers of large data blocks. The programmer always chooses from a set of compromises in attempting to satisfy often conflicting goals.

One difficult choice the programmer faces is portability versus efficiency. It is an agonizing one, too, because favoring efficiency results in nonportable code, while selecting portability often results in software whose performance is unsatisfactory.

Efficient software doesn't waste CPU cycles. It takes full advantage of the underlying hardware, often completely disregarding portability issues. It capitalizes on such features as graphics accelerators, cache memories, and specialized floating-point instructions.

Although efficient software is attractive from a purist's standpoint, the value of running the software on many different machine architectures tips the balance in the other direction. The reason is more financial than technical: in today's computing environments, software that runs on only one architecture sharply limits its potential marketability.

Building in portability doesn't mean that you must necessarily settle for inefficient, technically arcane software. To the contrary, obtaining optimum performance from portable software requires a higher level of technical sophistication. If the sophistication isn't there, however, you have an alternative in that you can wait until the hardware becomes available.

#### 4.1.1 Next _____'s hardware will run faster

We used to fill in the blank with "year": Next year's hardware will run faster. Because of the speed at which hardware technology races ahead, today we can sometimes say that next quarter's or even next month's hardware may run faster. The ever-shrinking product-development cycle of today's computer manufacturers allows them to produce newer models in a fraction of the time required in the past. Vendors leapfrog each other with frequent announcements of higher performance for a lower price. As a result, whatever computer you're using today will soon feel like the clunky old behemoth in the back of your college lab.

This tendency toward tighter design cycles will accelerate, too. Today's semiconductor designers use sophisticated simulators to create follow-on versions of their microchips. As these simulators themselves powerful computers continue to gain speed, developers can complete designs even more quickly. These newer chips then become the engines used in tomorrow's simulators. The phenomenon snowballs with each successive generation of silicon processors. The semiconductor-design world rides a dizzying, upward-bound performance spiral.

As faster machines replace slower ones, the critical issue then becomes not whether your software takes full advantage of all the features of the hardware, but whether your software will run on the newer machines. You might spend days or weeks tuning an application for better performance on today's platform, only to find that the next hardware upgrade gives you a factor-of-ten increase in speed “free.” However, your software must be portable to take advantage of the next supercomputer.

In the Unix environment, this usually translates into writing much software as shell scripts. A shell script consists of multiple executable commands placed in a single file executed indirectly by the Unix command interpreter. Because of the wide array of small, single-purpose commands found in a typical Unix distribution, all but the lowest level tasks can be constructed easily from shell scripts.

A side benefit of shell scripts is that they are far more portable than programs written in the C language. This may sound heretical, but writing your programs in C should be considered only if absolutely necessary. In the Unix environment, C lacks the portability of shell scripts. C programs often depend on definitions in header files, machine architecture sizes, and a host of other nonportable characteristics of a Unix implementation. As Unix was ported from 16-bit to 32-bit and 64-bit architectures, a significant amount of software became inoperable because C is not very portable. C is little more than the assembly language of the 1980s.

What if you want your program to run on other systems besides Unix? Other language choices exist, each with their peculiar strengths and drawbacks. If your goal is strictly one of portability, then Perl and Java fill the bill quite nicely, as implementations exist for both Unix and Windows platforms. However, just because a language has been ported to another platform besides Unix doesn't mean that the other platform adheres to the Unix philosophy and the Unix way of doing things. You will find that Java developers on Windows, for example, tend to be big proponents of interactive development environments (IDEs) that hide the complexity underneath, while Unix Java developers often prefer tools and environments that let them delve behind the graphical user interface.

#### 4.1.2 Don't spend too much time making a program run faster

If it barely runs fast enough, then accept the fact that it already meets your needs. All time spent tuning subroutines and eliminating critical bottlenecks should be done with an eye toward leveraging performance gains on future hardware platforms as well. Resist the tendency to make the software faster for its own sake. Remember that next year's machine is right around the corner.

A common mistake that many Unix programmers make is to rewrite a shell script in C to gain a marginal edge in performance. This is a waste of time better spent obtaining constructive responses from users. Sometimes a shell script may truly not run fast enough. However, if you absolutely must have high performance and believe that you need C to get it, think it over—twice. Certain specialized applications notwithstanding, it usually doesn't pay to rewrite a script in C.

Beware of “micro-optimizations.” If—and this is a very big “if”—you must optimize a C program’s performance, Unix provides prof and other tools for identifying the subroutines used most. Tuning routines called upon hundreds and thousands of times produces the greatest improvement for the least effort.
