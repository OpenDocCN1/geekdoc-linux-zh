RandomMlcgC wires RandomMlcgP.init in two different ways:

```
MainC.SoftwareInit -> RandomMlcgP; // Auto-initialize
Init = RandomMlcgP.Init; // Allow for re-initialization
```

In the first wiring, RandomMlcgC wires RandomMlcgP.init to the TinyOS boot sequence (MainC). When TinyOS boots, it calls MainC’s SoftwareInit.init, and so it calls RandomMlcgP’s Init.init. In the second, it equates its own RandomMlcgC.Init with RandomMlcgP.Init. If a component calls RandomMlcgC’s Init.init, it actually calls RandomMlcgP’s Init.init.

The first wiring makes sure that RandomMlcgP has been properly seeded before an application starts. If the application reseeds it by calling RandomMlcgC.Init or RandomMlcgC.SeedInit, no harm is done. But by wiring to MainC, RandomMlcgC makes sure that an application (or protocol, or system) doesn’t have to remember to initialize RandomMlcgC.

This technique – “auto-wiring” initialization – is used in many TinyOS abstractions. One very common bug in TinyOS 1.x was to forget to initialize. This usually happens because many components might be initializing the same component. This approach is wasteful, but since initialization only happens once, it’s not a huge issue. The bigger issue is that a component often relies on someone else initializing. For example, imagine two radio stacks, A and B. A initializes the timer system, B does not. A programmer writes an application using radio stack A and forgets to initialize the timer system. Because radio stack A does, everything works fine. The programmer then decides to switch to radio stack B, and nothing works: neither the application nor the stack initialize the timers, and so the system just hangs.

The init commands of components using auto-wired initialization are called in an arbitrary order (see Section 4.4 below). For software initialization – setting fields, etc. – this generally doesn’t matter (Init is not supposed to call anything besides another Init). Hardware initialization is a much trickier problem, and is generally handled on a per-platform basis. Refer to TEP 107 [14] for more details.

Programming Hint 12 Auto-wire Init to MainC in the top-level configuration of a software abstraction.

# 4.3 Component layering

RandomC shows how even a simple abstraction, such as a random number generator, can have several layers within it. On one hand, this programming style makes components small and reusable: for people who know them well, it makes building new systems the simple matter of combining existing building blocks and maybe adding a bit of new logic. On the other hand, it means getting to the bottom of a component – figuring out what it actually does – can be really frustrating to someone unfamiliar with the code. RandomC is a good example of this layering. A programmer, wanting to find the implementation (module code) of the random number generator, has to look at three files. RandomC points to RandomMlcgC, which points to RandomMlcgP.