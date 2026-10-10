
## IV.

change me was the fact that Transmeta was just about the most secretive company around. There was only one rule concerning what you could talk about, and that rule was very simple: "Say nothing." Which just made Linux people sometimes wonder what kind of strange cult I had joined, and whether I was ever coming back. I couldn't even tell my mother what I was up to— not that she would have been interested.

What I was doing at Transmeta wasn't all that strange. The first thing I actually ended up doing was fixing some of the Linux problems that Transmeta had. The company was using a lot of multiprocessor Linux machines. I had never personally worked on the Linux SMP (Symmetric MultiProcessing) issues, and it turned out that many things didn't really work the way they were supposed to. I took this as a personal affront, and had to fix it, of course.

But my real work was actually being part of the Transmeta softball team.

Oh, I mean software team. We didn't play all that much softball. None of the Silicon Valley leagues would let us join unless we agreed to tell them what we were up to.

I don't know how familiar people are with Transmeta. As I'm typing this, we're actually in our silent period before the (please, God, buy our stock) IPO, and we're no longer secret, although we're back in our stealth mode due to SEC rules about initial public offerings. Let's hope that by the time this book is out, everybody and his dog has heard about Transmeta and bought (subliminal message: STOCK) one or more of our CPUs. Because that's what Transmeta does—CPUs. Hardware.

But Transmeta does more than just hardware. Which is just as well because, quite frankly, I wouldn't know a transistor from a diode even if one kicked me in the head. What Transmeta does is *simple* hardware that relies on clever software to make a simple CPU look like much more than it really is—like a standard Intel-compatible x86, in fact. And with the hardware being made smaller and simpler, the CPU ends up having fewer transistors, which in turn makes it use less power, which as everybody realizes will become increasingly more important in a mobile world. This clever software is why Transmeta has a rather large software team, and why I was there.

This all fit me quite well. A non-Linux company that did something that was technically quite interesting (understatement of the year—I still don't know of another company that has ever seriously even tried to do what Transmeta does). And it was in an area that I knew intimately: low-level programming of the quite esoteric 80*86 family of CPUs. As you undoubtedly recall, it was the act of getting to know that CPU in the first personal computer I owned that had started the whole Linux project in the first place.

The fact that Transmeta wasn't a Linux company was also important to me. Don't get me wrong: I loved fixing Linux problems at Transmeta, and I've been involved in several internal projects about Linux. (In fact, these days it's probably impossible to find a serious technology company without such projects.) But at Transmeta, Linux was secondary—which was just what I wanted. I could continue to do Linux, but I didn't feel I would have to make the technical compromises that would favor the company's goals over Linux itself. I could continue to think of Linux as a hobby in which only technology mattered, and nothing else held sway over my decisions.

So during the day, I worked for Transmeta. I wrote and maintained the “*86 interpreter” that we still use today (although others maintain it now). The interpreter is basically the piece of Transmeta software that looks at Intel instructions one at a time, and executes them (i.e., it “interprets” the language of the 80*86 architecture, one instruction at a time). I ended up doing other things later, but that's how I got into the strange and wonderful world of hardware emulation.

During the night, I slept.

My deal with Transmeta was clear: I had been given vague assurances that I could work on Linux during work hours too. Trust me, I took full advantage of that.

A lot of people believe in working long days and doing double, triple, or even quadruple shifts. I'm not one of them. Neither Transmeta nor Linux has ever gotten in the way of a good night's sleep. In fact, if you want to know the honest truth, I'm a firm believer in sleep. Some people think that's just being lazy, but I want to throw my pillow at them. I have a perfectly good excuse, and I'm standing by it: You may lose a few hours of your productive daytime if you sleep, oh, say, ten hours a day, but those few hours when you are awake you're alert, and your brain functions on all six cylinders. Or four, or whatever.

### Welcome to Silicon Valley

One of the first things I got to do upon landing in this strange galaxy was to meet the stars.

I received an email from Steve Jobs's secretary about how he'd like to meet me and could I spare an hour or two. Not knowing what it was all about, I said sure.

The meeting was at Apple's headquarters on Infinity Loop Drive. It was with Jobs and his chief technical guy, Avie Tevanian. This was when Apple was starting work on OS X, the Unix-based operating system that wasn't released until September 2000. There wasn't much formality to the meeting. Basically, Jobs started off by trying to tell me that on the desktop there were just two players, Microsoft and Apple, and that he thought that the best thing I could do for Linux was to get in bed with Apple and try to get the open source people behind Mac OS X.

I stuck around because I wanted to learn about the new operating system. It's based on Mach, the microkernel developed at Carnegie Mellon University. In the mid-1990s the Mach was expected to be the ultimate operating system, and a lot of people were interested in it. In fact, IBM and Apple used Mach as the basis for their ill-fated Taligent joint-venture operating system.

Jobs made a big point of the fact that Mach's low-level kernel is open source. He sort of played down the flaw in the setup: Who cares if the basic operating system, the real low-core stuff, is open source if you then have the Mac layer on top, which is not open source?

He had no way of knowing that my personal opinion of Mach is not very high. Frankly, I think it's a piece of crap. It contains all the design mistakes you can make, and managed to even make up a few of its own. One of the arguments against microkernels has always been performance. So a lot of people did research projects aimed at determining how to turn microkernels into something that performs really well. All of the resulting recommendations made it into Mach. As a result, it became a very complicated system with rules of its own. And it still doesn't perform that well.

Avie Tevanian had been one of the Mach people when it was a university project. It was kind of interesting, discussing what he and Steve saw as the issues. At the same time, we disagreed fairly fundamentally on technical matters. I really didn't think there was a reason for open source or Linux people to get involved. Sure, I could understand why they wanted to get more open source developers into their system; they were seeing the momentum build behind Linux. But I don't think they were seeing it quite enough. I don't think Jobs realized that Linux would potentially have more users than Apple, although it's a very different user base. And I don't think Steve would be quite as eager to dismiss Linux as a desktop system today as he was three years ago.

I explained why I didn't like Mach. For understandable reasons that didn't go over very well. They'd certainly heard the arguments before. Obviously, I was very set on Linux and Tevanian was very set on Mach. It was interesting to see how they discussed some of the technical issues. One of the immediate problems I could see involved how they planned on supporting old Mac applications in the new operating system. They wanted to do all the old stuff with a compatibility layer. All the old Mac applications would run within one new tacked-on process. But one of the major shortcomings of the old Mac is the lack of memory protection, and this solution does nothing to solve that problem. Only the new Mac applications would have memory protection. It didn't make sense to me.
