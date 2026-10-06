
# Linux Administration: A Beginner's Guide

1960s that IBM considered selling application software. Through the 1950s and most of the 1960s, IBM considered software as merely a tool for enabling the sale of hardware. This return to openness was a wild departure from the early 1980s convention of selling prepackaged software, Stallman's concept of open source software was in line with the initial introductions of UNIX from Bell Labs. Early UNIX systems did full source code. Yet by the late 1970s, source code was typically removed from UNIX systems and could be acquired only by paying large sums to AT&T (now SBC). The Berkeley Software Distribution (BSD) maintained a free version, but its commercial counterpart, BSDI, had to deal with many lawsuits from AT&T until it could be proved that nothing in the BSD kernel came from AT&T.

# Kernel Differences

Each company sells a Linux distribution of its own will be quick to tell you its kernel is better than the others. How can a company make this claim? The answer comes from the fact that each company maintains its own patch set. To make sure that the kernels stay in sync, most companies adopt patches that are posted on www.kernel.org, the “Linux Kernel Archives.” Vendors, do not track the release of every single kernel that is released onto www.kernel.org. Instead, they take a foundation, apply their custom patches to it, run the kernel through their quality assurance (QA) process, and then take it to production. This helps organizations have confidence that their kernels have been sufficiently baked, mitigating any perceived risk of running open source-based operating systems.

The only exception to this rule revolves around security issues. If a security issue is found with a version of the Linux kernel, vendors are to adopt the necessary patches to fix the problem immediately. A new release of the kernel with the fixes is often within a short time (commonly less than 24 hours) so that administrators who install it can ensure their installations are secure.

Thankfully, if each vendor maintains its own patch set, what exactly is it patching? This varies from vendor to vendor, depending on each vendor's target market. Red Hat, for instance, is largely focused on providing enterprise-grade reliability and solid execution for application servers. This might be different from the mission of the Fedora team, which is more interested in trying new technologies quickly, and even more from the approach of a vendor that is trying to put together desktop-oriented or multimedia-focused Linux system.

What separates one distribution from the next are the value-added tools that come with each one. Asking, “Which distribution is better?” is much like asking, “Which is better, Coke or Pepsi?” Almost all colas have the same basic

# CHAPTER 1 Technical Summary of Linux Distributions

ingredients—carbonated water, caffeine, and high-fructose corn syrup—thereby giving the similar effect of quenching thirst and bringing on a caffeine-sugar buzz. In the end, it's a question of requirements: Do you need commercial support? Did your application vendor recommend one over another? Did the software (package) updating infrastructure suit your site's administrative style better than another distribution? When you review your requirements, you'll find that there is likely a distribution that is geared toward exact needs

The idea of giving away source code is a simple one: A user of the software should never be forced to deal with a developer who might or not support that user's intentions for the software. The user should never wait for bug fixes to be published. More important, code developed under the scrutiny of other programmers is typically of higher quality than code written behind locked doors. One of the greatest benefits of open source comes from the users themselves: They should need a new feature, you can add it to the original program and contribute back to the source so that everyone can benefit from it.

This line of thinking sprung a desire to release a complete UNIX-like system (Linux) to the public, free of license restrictions. Of course, before you can build any system, you need to build tools. And this is how the GNU project and its namesake license were born.

> NOTE GNU stands for GNU's Not—recursive acronyms are part of hacker humor. If you don't understand why it's funny, don't worry. You're still in the majority.

# The GNU Public License

An important thing to emerge from the GNU project is the GNU Public License (GPL). This license explicitly states that the software is released free and no one can ever take away these freedoms. It is acceptable to take the software and resell it, even for a profit; however, in this resale, the seller must release the full source code, including any changes. Because the resold package remains under the GPL, the of primary importance is the liability clause: The programmers are not liable for any damages caused by their software.

It should be noted that the GPL is not the only license used by open source developers (although it is arguably most popular). Other licenses, as BSD and Apache, have similarity clauses but differ in terms of their redistribution. For instance, the BSD license allows people to make changes to the code and ship them without having to disclose the added code. (Whereas the GPL requires that the added code is shipped.) For more information about other open source licenses, check out www.opensource.org.

# Historical Footnote

Many moons ago, Red Hat started a commercial offering of its erstwhile free product (Red Hat Linux). The commercial release gained steam with the Red Hat Enterprise Linux (RHEL) series. Because the foundation for RHEL is GPL, individuals interested in maintaining a free version of Red Hat's distribution have been able to do. Furthermore, as an outreach to the community, Red Hat created the Fedora Project, which is considered the testing grounds for new software before it is adopted by the RHEL team. The Fedora Project is freely distributed and can be downloaded from http://fedoraproject.org or https://getfedora.org.

# Upstream and Downstream

To help you understand the concept of upstream and downstream components, let's start with an analogy. Picture, if you will, a pizza with all your favorite toppings.

The pizza is put together and baked by a local pizza shop. Several things go into a great pizza—cheeses, vegetables, flour (dough), herbs, meats, to mention a few. The pizza shop will often make some of these ingredients in house and rely on other businesses to supply other ingredients. The pizza shop will also be tasked with assembling the ingredients into a complete finished pizza.

Let's consider one of the most common pizza ingredients—cheese. The cheese is made by a cheesemaker who makes cheese for many other industries or operations, including the pizza shop. The cheesemaker is pretty set in her ways and has very strong opinions about how her product should be paired with other food stuffs (wine, crackers, bread, vegetables, and so on). The pizza owners, on the other hand, do not care about other stuffs—the pizza shop will bump heads because of differences in opinion and objectives. At other times they will be in agreement and cooperate beautifully. Ultimately (and sometimes unknown to them), the pizza owners and cheesemaker care about the same thing: producing the product that they can.

The pizza shop in our analogy represents the Linux distributions/projects (Fedora, Debian, RHEL, openSE, and so on). The cheesemaker represents the software project maintainers who provide the important programs and tools (such as the Bourne Again Shell [Bash], GNU Image Manipulation Program [IMP], GNOME, KDE, Nmap, and GNU Compiler Collection [GCC]) that are packaged together to make a complete distribution (pizza). The Linux distribution vendors are referred to as the downstream component of the open source food chain; the maintainers of the accompanying software projects are referred to as the upstream component.
