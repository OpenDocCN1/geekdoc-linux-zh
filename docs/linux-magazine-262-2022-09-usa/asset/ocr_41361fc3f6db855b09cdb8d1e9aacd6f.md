# Zack's Kernel News

![](bbox=[0.07, 0.19, 0.31, 0.36])

> Chronicter Zack Brown reports on the latest news, views, dilemmas, and developments within the Linux kernel community.
> *By Zack Brown*

# Random Number Sanity

Random numbers are important for security. Generally to make random numbers, you grab entropy from somewhere, like the frequency of fingers tapping a keyboard, and use that to generate as many unpredictable numbers as needed. But what if no one's typing on the keyboard? What if you run out of entropy? Should the system just sit and wait for more?

For a long time, the Linux kernel had to choose between locking up the system until it found enough entropy to make truly random numbers and providing numbers anyway, even if they weren't really random enough.

But in 2019, Linus Torvalds wrote a patch that addressed the problem "by actively generating entropy noise using

the CPU cycle counter when waiting for the random number generator to initialize. This only works when you have a high-frequency time stamp counter available, but that's the case on all modern x86 CPUs, and on most other modern CPUs too.

Because of that patch, the random number generator would pretty much always have enough entropy to produce useful random numbers. Recently, Jason A. Donenfeld felt it was time for everyone to admit it was working, get over their mistrust of technology and new things, and allow the Linux random number generator to block while building up entropy.

This is inherently a controversial topic. If the system waits for a resource that never becomes available, it'll just wait forever, and then you've got a brick on your hands. There have been various attempts to introduce blocking into the random number generator, but they were taken out shortly after going into the source tree.

But Jason said, "given that the kernel has grown this mechanism for seeding itself from nothing, and that this process happens pretty fast, maybe there's no point any longer in having /dev/urandom give insecure bytes. In the past we didn't want the boot process to dead-lock, which was understandable. But now, in the worst case, a second goes by, and the problem is resolved. It seems like maybe we're finally at a point when we can get rid of the infamous 'urandom read hole.'"

He added, "This patch goes a long way toward eliminating a long overdue userspace crypto footgun. After several decades of endless user confusion, we will finally be able to say, 'use any single one of our random interfaces and you'll be fine. They're all the same. It doesn't matter.' And, I, think, is really something. Finally all of those blog posts and disagreeing forums and contradictory articles will all become correct about whatever they happened to recommend, and along with it, a whole class of vulnerabilities eliminated."

The "footgun" Jason mentioned is not some kind of obscure security-related attack vector; it's just slang for something that makes it easy to shoot yourself in the foot.

But Andy Lutomirski made just about the strongest possible objection that anyone can make against a Linux kernel patch - saying that it violated the application binary interface (ABI) - and while doing it he offered some historical perspective on this whole issue. He said:

"This patch is 100% about a historical mistake. Way back when (not actually that long ago), there were two usable interfaces to the random number generator: /dev/random and /dev/urandom. /dev/random was, at least in principle, secure, but it blocked unnecessarily and was, therefore, incredibly slow. It was totally unsuitable for repeated use by any sort of server. /dev/urandom didn't block but was insecure if called too early. *But* urandom was also the correct interface to get best-effort-I-need-them-right-now random bits. The actual semantics that general cryptography users wanted were not available.

"Fast forward to today. /dev/random has the correct semantics for cryptographic purposes. getrandom() also has the correct semantics for cryptographic purposes and is reliable as such - it is guaranteed to either not exist or to DTRT (do the right thing). And best-effort users can use GRND_INSECURE or /dev/urandom.

"If we imagine that every user program we care about uses GRND_INSECURE for best-effort and /dev/random or getrandom() without GRND_INSECURE for cryptography, then we're in great shape and this patch is irrelevant.

"But we don't get to rely on that. New kernels are supposed to be compatible with old userspace. And with *old* userspace, we do not know whether /dev/urandom users want cryptographically secure output or whether they want insecure output. And there is this unwind during boot that lasts, supposedly, up to 1 second; there is a massive difference. So, sorry, this patch is an ABI break. You're reinterpreting any program that

# Author

The Linux kernel mailing list archives the core of Linux development activities. Traffic volumes are immense, often reaching 10,000 messages a week, and keeping up to date with the entire scope of development is a virtually impossible task for one person. One of the few brave souls to take on this task is **Zack Brown**.