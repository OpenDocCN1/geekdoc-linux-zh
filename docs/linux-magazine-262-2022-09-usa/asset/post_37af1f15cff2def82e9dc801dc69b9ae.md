
## Zack's Kernel News

![](img/b40e8bf6cf651f8eebf36f5265123095_11_0.png)

> Chronicler Zack Brown reports on the latest news, views, dilemmas, and developments within the Linux kernel community.
> *By Zack Brown*

### Random Number Sanity

Random numbers are important for security. Generally to make random numbers, you grab entropy from somewhere, like the frequency of fingers tapping a keyboard, and use that to generate as many unpredictable numbers as needed. But what if no one's typing on the keyboard? What if you run out of entropy? Should the system just sit and wait for more?

For a long time, the Linux kernel had to choose between locking up the system until it found enough entropy to make truly random numbers and providing numbers anyway, even if they weren't really random enough.

But in 2019, Linus Torvalds wrote a patch that addressed the problem "by actively generating entropy noise using the CPU cycle counter when waiting for the random number generator to initialize. This only works when you have a high-frequency time stamp counter available, but that's the case on all modern x86 CPUs, and on most other modern CPUs too."

Because of that patch, the random number generator would pretty much always have enough entropy to produce useful random numbers. Recently, Jason A. Donenfeld felt it was time for everyone to admit it was working, get over their mistrust of technology and new things, and allow the Linux random number generator to block while building up entropy.

This is inherently a controversial topic. If the system waits for a resource that never becomes available, it'll just wait forever, and then you've got a brick on your hands. There have been various attempts to introduce blocking into the random number generator, but they were taken out shortly after going into the source tree.

But Jason said, "given that the kernel has grown this mechanism for seeding itself from nothing, and that this process happens pretty fast, maybe there's no point any longer in having /dev/urandom give insecure bytes. In the past we didn't want the boot process to dead-lock, which was understandable. But now, in the worst case, a second goes by, and the problem is resolved. It seems like maybe we're finally at a point when we can get rid of the infamous 'urandom read hole.'"

He added, "This patch goes a long way toward eliminating a long overdue userspace crypto footgun. After several decades of endless user confusion, we will finally be able to say, 'use any single one of our random interfaces and you'll be fine. They're all the same. It doesn't matter.' And, I think, that is really something. Finally all of those blog posts and disagreeing forums and contradictory articles will all become correct about whatever they happened to recommend, and along with it, a whole class of vulnerabilities eliminated."

The "footgun" Jason mentioned is not some kind of obscure security-related attack vector; it's just slang for something that makes it easy to shoot yourself in the foot.

But Andy Lutomirski made just about the strongest possible objection that anyone can make against a Linux kernel patch - saying that it violated the application binary interface (ABI) - and while doing it he offered some historical perspective on this whole issue. He said:

"This patch is 100% about a historical mistake. Way back when (not actually that long ago), there were two usable interfaces to the random number generator: /dev/random and /dev/urandom. /dev/random was, at least in principle, secure, but it blocked unnecessarily and was, therefore, incredibly slow. It was totally unsuitable for repeated use by any sort of server. /dev/urandom didn't block but was insecure if called too early. *But* urandom was also the correct interface to get best-effort-I-need-them-right-now random bits. The actual semantics that general cryptography users wanted were not available.

"Fast forward to today. /dev/random has the correct semantics for cryptographic purposes. getrandom() also has the correct semantics for cryptographic purposes and is reliable as such - it is guaranteed to either not exist or to DTRT (do the right thing). And best-effort users can use GRND_INSECURE or /dev/urandom.

"If we imagine that every user program we care about uses GRND_INSECURE for best-effort and /dev/random or getrandom() without GRND_INSECURE for cryptography, then we're in great shape and this patch is irrelevant.

"But we don't get to rely on that. New kernels are supposed to be compatible with old userspace. And with *old* userspace, we do not know whether /dev/urandom users want cryptographically secure output or whether they want insecure output. And there is this unwind during boot that lasts, supposedly, up to 1 second; there is a massive difference. So, sorry, this patch is an ABI break. You're reinterpreting any program that wanted best-effort randomness right after boot as wanting cryptographic randomness, this can delay boot up by 1 second, and that’s more than enough delay to be considered a break.

“So I don’t like this without a stronger justification and a clearer compatibility story. I could “maybe” get on board if you had a `random=***` option to switch back to the old behavior and a very clear message like ‘random: startup of %s is delayed. Set random=*** for faster boot if you do not need cryptographically secure random during boot,’ but I don’t think this path is okay otherwise.”

“Or we stick with the status quo and make the warning clearer: 'random: %s us using insecure random output. Fix it to use getrandom() or /dev/urandom as appropriate.'”

So Andy wasn’t disputing that Jason’s patch could work — he was pointing out that it would change the system behavior in ways that might break existing compiled user-space binaries. In other words, it would break the kernel ABI. If true, Jason’s patch would have a giant hurdle to clear. In general, the only thing Linux hates worse than breaking the ABI is allowing a security hole to go unpatched. But if it can be shown that no users rely on a particular piece of the ABI, Linus has been known to allow a patch to change it.

In this case, Jason said to Andy:

“*I think your analysis is a bit mismatched from the reality of the situation. That reality is that cryptographic users still find themselves using /dev/random, as that’s been the ‘standard good advice’ for a very long time. And people are still encouraged to do that, either out of ignorance or out of ‘compatibility.’ The cryptographic problem is not going away. Fixing this issue means, yes, adding a 1 second delay to the small group of init system users who haven’t switched to using getrandom(GRND_INSECURE) for that less common usage (who even are those users actually?). That’s not breaking compatibility or breaking user-space or breaking anything; that’s accepting the reality of how /dev/random is mostly used — for crypto — and making that usage finally secure, at the expense of a 1 second delay for those other users who haven’t switched to getrandom(GRND_INSECURE) yet. That seems like a very small price to pay for eliminating a footgun.

“And, in general, dephasizing the rare performance of the less common usage in favor of fixing a commonly triggered footgun seems on par with how things morph and change over time. There’s no actual breakage. There’s no ABI change violation. What you’re saying simply isn’t so.*”

Theodore Ts’o joined the discussion on Jason’s side of the argument. He said, “So long as we’re only blocking for short amounts of time, and only during early after the system was booted, people shouldn’t care. The reason why we had to add the ‘gee-I-hope-this-jitter-entropy-like-hack-is-actually-secure on all architectures but it’s better than the alternatives people were trying to get Linux to adopt’ was because there were systems that were hanging for hours or days.”

But the proof is in the pudding, and a week or so after Jason’s patch went into the kernel tree, Guenter Roeck pointed out that it caused “a large number of qemu boot test failures for various architectures (arm, m68k, microblaze, sparc32, x86: are the ones I observed). Common denominator is that boot hangs at ‘Saving random seed.’ A sample bisection log is attached. Reverting this patch fixes the problem.”

At this point Linus joined the conversation, saying, “OK, it was worth trying, but yeah, it clearly causes problems for various platforms that can’t do jitter entropy and have nothing else happening either.”

And he reverted the patch.

Jason also commented on Guenter’s post, saying, “As Linus said, it wasn’t worth a try, and I guess it just didn’t work.”

But the story didn’t end there. Jason asked Guenter to share some of the virtual machines that seemed to break with the patch, and the two of them — and others — proceeded to track down the real reasons why Qemu had a problem with Jason’s patch. As Jason put it, “if we do ever reattempt this sometime down the road, it seems like understanding everything about why the previous time failed might be a good idea.”

In fact, it turned out to be a Qemu bug, rather than a problem with Jason’s random number generation modifications. To Jason, this meant that “the rationale for reverting the /dev/random + /dev/urandom unification has now been fixed. That’s some real tangible progress.”

But he remained cautious. Jason went on to say, “I don’t want to rush into trying the unification again too soon. I think at anyhimp, the lesson from the first attempt wasn’t simply, I should fix a few of Guenter’s test cases,” but rather that the problem is “early queued, and take a lot wider testing and research. However, the fact that the initial thing, across multiple platforms, that lead to the revert has been fixed gives me a decent amount of optimism, that at /some point/ down the road, we’ll be able to try this thing. One step at a time.”

Ultimately, it seems that Linus does not consider the issue in its entirety to be an unacceptable ABI violation. And he is willing, if not eager, to take something like Jason’s patch if it works. So in theory, Jason may be bringing a little more sanity to random number generation in the near future.

### Git Lesson from Linus

Borislav Petkov submitted a pull request to Linus Torvalds against the 5.18 kernel tree, but he noticed that his workflow had resulted in a strange diffstat. Diffstats are auto-generated summaries of which files were changed and by how much. It’s one way the kernel developers can quickly see which parts of a patch might interest them. In this case, Borislav noticed Git complaining about “multiple merge bases,” and he described what he thought he had done to produce that complaint:

“I needed to have prerequisite work from another tip branch: tip/locking/core which was fast-forwarded to v5.17-rc1 before I got that prerequisite work added onto.

“so I merged tip/locking/core into tip/ras/core […] and added the RAS stuff onto

“*However, when creating the diffstat for the pull request, it would add additional files to it from tip/locking/core even if all the tip/locking/core changes are already in your master branch.*”

He didn’t see exactly what he had done wrong, so he asked Linus for an explanation. Linus replied:

“*What you are describing is a very fundamental thing — your branch has multiple separate starting points, since you*”

### Author

The Linux kernel mailing list archives the core of Linux development activities. Traffic volumes are immense, often reaching 10,000 messages a week, and keeping up to date with the entire scope of development is a virtually impossible task for one person. One of the few brave souls to take on this task is **Zack Brown**.
