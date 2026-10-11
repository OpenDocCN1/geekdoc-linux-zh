# # Going In or Going Out?

An ongoing question in operating systems development is which is better: a micro-kernel or a monolithic kernel? The debate is a little odd since there is no clear definition of a monolithic kernel, although everyone seems to agree Linux is one.

The microkernel camp, in the open source world, is the GNU project with its Hurd microkernel. The idea of a micro-kernel is that user space should do as much work as possible and that only the bare minimum functionality should be implemented in the kernel itself. By doing it this way, the microkernel people argue that it’s possible to produce a highly secure system because the kernel has fewer attack vectors. The smaller scope will mean fewer code churn over time and therefore fewer bugs that might be exploited by attackers.

The debate is odd because it frames the question in terms of efficiency and safety versus total chaotic insanity. In fact (and also the subject of this column), pretty much everyone wants their operating system kernel to be as small as possible for exactly those same reasons. Perhaps the debate really ought to be over exactly what belongs in user space and what doesn’t.

For example, in the Linux Kernel Mailing List recently, Shijie Huang posted some non-uniform memory access (NUMA) patches. NUMA is a multiprocessor hardware architecture like symmetric multiprocessing (SMP). But whereas SMP hides the differences between the memory and CPUs that might be in use at any given time, NUMA can have some hardware that is faster than others. For consumer products, this means less expensive manufacturing. The question for operating system developers is how to support the allocation process so that faster hardware is used when needed and slower hardware is used when speed isn’t as important.

Shijie’s patch addressed the need for the OS to be aware of which hardware, and therefore which speeds, would be used for a given task. For example, a given file loaded into memory would have only one cached version of itself, in spite of the fact that there were multiple hardware speeds that might be relevant to using that cached version.

Shijie wanted users to be able to specify the NUMA needs of any given file, or the kernel would use the faster or slower hardware whenever it needed to access that file. In other words, he asked, “is it possible to implement the per-node page cache for programs/libraries?”

This, however, was easier said than done, as you might imagine, controlling which hardware would operate on a given file takes place in a fairly deep part of the kernel. As Matthew Wilcox put it in his response:

> *“At this point, we have no way to support text replication within a process. So what you’re suggesting (if implemented) would work for processes which limit themselves to a single node. That is, if you have a system with CPUS 0-3 on node 0 and CPUs 4-7 on node 0, a process which only works on node 0 or only works on node 1 will get text on the appropriate node.*

> *“If there’s a process which runs on both nodes 0 and 1, there’s no support for per-node PGDs. So it will get a mix of pages from nodes 0 and 1, and that doesn’t necessarily seem like a big win.*

Al Viro also replied to Shijie, saying, “What you me mean, per-node page cache? Multiple pages for the same area of file? That’d be bloody awful on coherency…”

Coherence is a crucial part of operating system design – it means that when the kernel writes to a piece of memory, subsequent attempts to read that same piece of memory should show the write value rather than show an older value that was there before the write. Loss of memory coherence in an operating system is sort of the equivalent of suddenly discovering the building you’re in is engulfled in flames.

Shijie agreed that coherence was important, but he said that if the data was restricted to being read-only, coherence wouldn’t be a problem because the values would never change. He posted a patch to demonstrate what he was talking about.

Linus Torvalds came in at this point, saying, “You absolutely don’t want to actually duplicate it in the cache.”

There was some implementation discussion between Shijie and various others, but at one point Linus came in again, a bit harder, saying:

> *“You can’t have no-node I_mapping pointers without huge coherence issues.*

> *“If you don’t care about coherence, that’s fine – but that has to be a user-space decision (ie “I will just replicate this file”).*

> *“You can’t just have the kernel decide “I’ll map this set of pages on this node, and that other (set) of pages that that other node”, in case they’re MAP_SHARED things going on.*

> *“Anyway, I think very fundamentally this is one of those things where 99.9% of all people don’t care, and DO NOT WANT the complexity.*

> *“And the 0.1% that _does_ care really could and should do this in user space, because they know they care.*

> *“Asking the kernel to do complex things in critical core functions for something that is very very rare and irrelevant to most people, and that can and should just be done in user space for the people who care is the wrong approach.*

> *“Because the question here really should be ‘is this truly important, and does this need kernel help because user space simply cannot do it itself?’*“

> *“And the answer is a fairly simple ‘no’.*

The discussion ended at that point, and Shijie went back to the drawing board.

For me, this is an example of a feature that could have gone into the monolithic Linux kernel. It would have performed a useful function for a certain bunch of users. It would have handled use cases that exist in the real world. It would have made the kernel as a whole slower, but it would be exactly the sort of thing the microkernel people would expect a monolithic kernel to include.

It seems very clear that proponents of both microkernels and monolithic kernels believe that if something can be done in user space, then it shouldn’t be put into the kernel. And the point of difference becomes what exactly do we use to draw the line? At this point, it becomes largely a matter of personal opinion. Linus would probably say that it depends on a lot of factors. Can the feature run much faster in the kernel than in user space? Will the kernel code look sane and be maintainable? And so on. And probably the GNU Hurd people would have different opinions, as would the Redox people, the Genode people, the HelenOS people, and the contributors to various other micro-kernel projects.