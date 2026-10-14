
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

## 4.3 Component layering

RandomC shows how even a simple abstraction, such as a random number generator, can have several layers within it. On one hand, this programming style makes components small and reusable: for people who know them well, it makes building new systems the simple matter of combining existing building blocks and maybe adding a bit of new logic. On the other hand, it means getting to the bottom of a component – figuring out what it actually does – can be really frustrating to someone unfamiliar with the code. RandomC is a good example of this layering. A programmer, wanting to find the implementation (module code) of the random number generator, has to look at three files. RandomC points to RandomMlcgC, which points to RandomMlcgP.

### 4.3.1 Extensibility

In practice, these layers of indirection are not particular to nesC: any system with complex libraries has them. The difference is how those layers are written. In C code, you might see a series of functions that are simple wrappers (e.g. printf as a call to fprintf passing stdout as the file stream): you traverse executable code. In nesC code you traverse namespace mappings through configurations. The first few times you try to get to the bottom of a function, this difference can be a bit confusing, but it doesn't take very long to get used to it. You can also use the nesC's nesdoc tool to navigate through an application's wiring and find where an interface is ultimately implemented – see the TinyOS tutorials for more information.

Just as in other languages, especially object-oriented ones, nesC software design has a tension between how simple the implementations are and how easy it is to use or reuse them. The C++ standard template library is infamous for this: it is amazingly powerful, general, and efficient, but understanding the implementations is non-trivial. Putting all of a system's functionality in a single module means a user doesn't need to track down call chains. But it means that modifying the system requires replacing or copying that entire file. This leads to code replication, which greatly increases the lifetime of software bugs (if there's a bug in the copied code, you need to change all of the copies, and almost always forget one). Therefore, a lot of the core TinyOS abstractions, such as timers and communication, tend to be composed of many small components. This makes the systems more difficult to understand at a first read, but easy to tweak, replace, or modify once you do.

### 4.3.2 Hardware specificity

Furthermore, there's a tension between high-level APIs that are hardware independent and APIs that enable a program to take advantage of all of the hardware capabilities. For example, some but not all radios have multiple channels (frequencies). Some systems may want to take advantage of this functionality, and are willing to assume they are using a particular radio chip in order to do so. Other systems may want to remain hardware independent.

TinyOS uses component layering to make this possible. Let's look at packet communication as an example. The top-level component a platform needs to provide is called ActiveMessageC and is hardware independent.¹ ActiveMessageC is almost always a configuration that layers on top of a chip-specific component that provides additional interfaces. For example, this is the implementation of ActiveMessageC for the micaz mote, which has a CC2420 radio chip:

```
configuration ActiveMessageC {
  provides {
    interface SplitControl;
```

¹ TinyOS uses "active messages" [29], often abbreviated to AM, as its networking abstraction (see Section 6.3).
