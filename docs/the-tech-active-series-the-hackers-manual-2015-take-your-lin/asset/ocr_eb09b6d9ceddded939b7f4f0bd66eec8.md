# Set up a secure VPS

![](bbox=[0.22, 0.34, 0.82, 0.62])

# Stay thy LAMP stack-installing hand a moment while we give you a primer on virtual private server security.

Virtual servers are cheap. In fact, with a few usage provisos, you can get one from Amazon for free and having your own virtual server is a great way to learn about all the responsibilities, pitfalls and street credits associated with remotely administering your own internet-facing box, without having to worry about failing hardware and hefty server bills.

Except for Amazon’s free usage tier, the cheapest virtual machines (VMs) out there run on what’s known as operating system-level virtualisation technology. The most abundant example is OpenVZ (Open Virtuozzo), which runs a modified Linux kernel that’s shared among all the guest OSes (OpenVZ only supports Linux guests, but why would you want anything else?).

> "Hypervisor relates to the fact that operating systems were once referred to as supervisors."

OpenVZ is close to being an example of a hosted (Type 2) hypervisor, since it runs inside a conventional OS. However, purists would argue that it doesn’t really do true virtualisation, but rather containerisation – being more akin to supervising a bunch of chroot environments rather than actual OSes. Incidentally, the etymology behind the word hypervisor relates to the fact that operating systems were once referred to as ‘supervisors’. Hence, a hypervisor is a supervisor of supervisors.