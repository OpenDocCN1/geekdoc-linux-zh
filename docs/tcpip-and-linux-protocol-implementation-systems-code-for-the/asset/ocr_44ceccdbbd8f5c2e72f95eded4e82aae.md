around the code with help of (course) from the Linux Documentation Project,
and from a variety of tools (ctags and vi, etags and emacs, the Red Hat source
code navigator, grep, ls-R, find, and so on—all those things that make UNIX-like
systems the tools of choice for systems developers).

# Roadmap, Outline, and Organization

The book is in 10 chapters. Chapter 1 is a very brief reminder of the way that the
Internet Protocol suites works. Chapter 2 is an introduction to the Linux operating
system kernel. Chapter 3 is a walk-through of the life cycle of a single packet,
from creation to transmission, and from reception to consumption. Chapter 4
is a recapitulation of Interprocess communication; in other words, an overview
of socket programming. Chapter 5 is about the kernel infrastructure support for
communications in general. Chapter 6 is a walk-through of the implementation
of the network layer and code. Chapter 7 is about transport protocol
implementations. Chapter 8 covers routing, while Chapter 9 is about the rich
Linux support for different packet forwarding treatments. We wrap up with
Chapter 10, which is about network security, covering various network filtering
techniques and applications.

The approach taken is largely code-centric, but with explanations and illus-
trations of the way the code fits together and is used by other layers.

Each chapter covers the concepts and implementation from one or more of
five perspectives:

+   **Data structures.** We show by example the way that protocol state and
packet data is stored.

+   **Wire format of packets.** We show the format of packets as transmitted/
forwarded/received.

+   **Algorithm/code.** The rules for processing user, network, and timer events
are detailed.

+   **Process.** The progression of the set of tasks involved in communication are
illustrated.

+   **Operational.** We cover the set of actions carried out by the system
manager, network manager, and an ordinary user.

The structure of most chapters covers these five perspectives, and then-
nects them together through a story—the life of some component activity of the
Internet Protocol architecture as exemplified by the Linux implementation.