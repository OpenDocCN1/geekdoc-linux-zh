
per second.

- An electric utility had one system that was the central controller for the electric power grid of one of the largest states in the United States. An outage would leave millions of people without power until the system was fixed.

The Unix developers certainly didn't know what would happen to Unix. Nor did the developers of MS-DOS, OpenVMS, and every other operating system for that matter. Every new OS—and Linux is no exception—takes its designers into uncharted waters. Their only hope consists of continually gathering progress reports and then correcting the course accordingly.

For example, did Ken Thompson realize the importance of portability when he wrote the first Unix kernel? Evidently not, for he wrote early Unix kernels in assembly language. He rewrote them later in a higher-level language, altering his original direction. Did Dennis Ritchie anticipate that C would become a universal programming language, loved and abhorred by millions of programmers? Hardly. The reissue of his classic *The C Programming Language* contained modifications to the language specification that affirmed that he didn't get it right the first time either.

So most of us are still learning. Even if we're egotistical enough to think that we know it all, someone will change the requirements on us. How then are we to build software? The next tenet holds the key.

[1] One of the simplest of all Unix commands, cat, directs everything that a user types into a file. Unlike a text editor or word processor, however, the cat command doesn't allow one to modify the text on previous lines.

## 3.2 Tenet 3: Build a prototype as soon as possible

When we say "as soon as possible," we mean as soon as possible. Post haste. Spend a small amount of time planning the application, and then get to it. Write code as if your life depended on it. Strike while the computer is warm. You haven't a nanosecond to waste!

The idea runs counter to what many would consider "proper engineering methodology." Most have been told that you should fully design an application before embarking on the coding phase. "You must write a functional specification," they say. "Hold regular reviews to ensure that you're on track. Write a design specification to clarify your thoughts on the details. Ninety percent of the design should be done before you ever fire up the compiler."

These guidelines sound fine in principle, but they fail to place enough emphasis on the prototype. It is in the building of the prototype that the idea is first tested for merit in a visual, realistic way. Before then, you have little more than a collection of thoughts about the way something ought to work. The concept is barely understood at that point, and it is highly unlikely that everyone perceives it in the same way. You need a consensus of perception before the project can proceed. The prototype moves toward that consensus by providing a concrete representation of the goal.

### 3.2.1 Prototyping is a learning process

The sooner it begins, the closer you will be to the released product. The prototype shows you what works and, most important, what doesn't. You need this affirmation or denial of the path you've chosen. It is far better to discover a faulty assumption early and suffer only a minor setback than to spend months in development meetings unaware of the Mother of All Design Flaws waiting to ambush you three weeks before the deadline.

### 3.2.2 Early prototyping reduces risk

Suppose you have something concrete that you can point to, and say "It's going to look like this." If you can show it to trusted users to get their reactions, you may learn that your design was on target. More often than not, your prototype will come back shot full of holes. That's OK, though. You have gained valuable design information. It is better to weather the ripples of a small group of critics than to hear a million users screaming for a recall of your product.

For every correct design, there are hundreds of incorrect ones. By knocking out a few of the bad ones early, you begin a process of elimination that invariably brings you closer to a quality finished product. You discover algorithms that do not compute, timings that keep missing a beat, and user interfaces that cannot interface. These trials serve to winnow out the chaff, leaving you with solid grain.

Most people agree that prototyping has many advantages. Even the academics who teach more traditional software engineering methodologies readily recognize its value. However, prototyping is a means to an end, not the end in itself. The goal of all prototyping should be to build something we call the Third System. Before we can talk about the Third System, though, we need to talk about the two systems that came before it.

## 3.3 The Three Systems of Man

Man has the capacity to build only three systems. No matter how hard he may try, no matter how many hours, months, or years for which he may struggle, he eventually realizes that he is incapable of anything more. He simply cannot build a fourth. To believe otherwise is self-delusion.

Why only three? That is a tough question. One could speculate on several theories drawn from scientific, philosophical, and religious viewpoints. Each could offer a plausible explanation for why this occurs. But the simplest explanation may be that the design process of man's systems, like man himself, passes through three stages of life: youth, maturity, and old age.

In the youthful stage, people are full of vigor. They are the new kids on the block; they exude vitality, crave attention, and show lots of potential. As a person passes from youth to maturity, he or she becomes more useful to the world. Careers take shape. Long-term relationships develop. Influence widens in worldly affairs. The person makes an impact—good, bad, or otherwise. By the time old age sets in, the person has lost many abilities of youth. As physical prowess declines, much of the person's worldly influence fades as well. One's career becomes a memory. Resistance to change sets in. What remains is valuable wisdom based on experience.

Man's systems pass through these same stages in their development. Each system possesses characteristics that correlate with corresponding periods in life. All systems follow a path beginning at youth, transiting through maturity, and ending in old age.

Just as some men and women never reach old age, so some systems fail to mature as well. Often, this is due to external circumstances. Development plans may change. Funding for a project may be withdrawn. A potential customer may change his mind and decide to shop somewhere else. Any number of these factors could serve to prevent the system from reaching maturity. Under normal conditions, though, man carries the systems through all three stages. For our purposes, we refer to these stages as the Three Systems of Man.

Most Unix developers don't know the Three Systems of Man by name, but they readily attest to their existence. Let's take a closer look at some of their characteristics.

## 3.4 The First System of Man

### 3.4.1 Man builds the First System with his back against the wall

Usually the developer is under pressure to meet a deadline or satisfy other time-critical demands. This ignites a creative spark within him. Eventually the spark becomes a small flame as he spends hours in intense deliberation, turning the idea over repeatedly in his mind. Work continues. His creative instincts begin to really take hold. The flame grows brighter.

At some point, he becomes aware of aspects of his idea that go beyond simply reaching his goal. He feels as though he has stumbled upon something far more significant. The goal fades somewhat, but not before he has convinced himself that his idea provides the solution.

### 3.4.2 He has no time to do it right

If he had the time to do it right, he wouldn't be under any deadline pressure. So he has to improvise. But whereas the typical improvisation is one of compromise, this effort roars ahead without compromise—in the wrong direction. At least, that is what his observers conclude. When a developer's back is against the wall without time to do it right, he tends to break all the rules. It appears to his traditional-thinking coworker that he has lost his marbles under the refrigerator.

Critics often rise against him. "He can't get away with that!" they insist. "He doesn't know what he's doing. He's going about it all wrong." His response? "Yeah, it's ugly, but it works!"

The lack of time to do it right forces him to focus on the important aspects of the task and to ignore the nonessentials. As a result, he plans to leave some details to include in later versions. Note that he may never complete any later versions. The belief that he will "fill in the blanks" in the future, however, keeps him from becoming sidetracked and also provides an excuse for any shortcomings in the first version.

### 3.4.3 Man builds the First System alone or, at most, with a small group of people

This is partly because many people in the mainstream have little appreciation for what he's doing. They have not seen what he has seen from his vantage point, so they have no idea why he's excited. Hence, they conclude that his work is interesting, but not interesting enough for them to get involved.

A second reason that many people avoid working on the First System is more practical: Building the First System involves significant risk. No one knows whether the First System will have the characteristics that lead to the development of the Second System. There always exists a better than 80 percent chance of failure. Being associated with a First System that failed can be "career limiting," in industry jargon. Consequently, some people would rather wait until the idea is proven. (They usually become the developers of the Second System. More about them later.)
