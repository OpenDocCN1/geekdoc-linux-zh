# Distro Walk — Trisquel

Guidelines (FSDG) [5]. This is different from the SF's Respects Your Freedom (RYF) list, which is a program for the certification of hardware products – that is, devices that don't require non-free components such as proprietary firmware or drivers to work [6]. The FSDG is a set of recommendations given by the GNU project to produce distributions of GNU that follow the principles of the project. Distributions that follow the guideline are recommended by the FSF and GNU and are used (and sometimes produced) by vendors that are RYF certified, so there is an overlap.

The distributions recommended by the FSF and GNU are mostly listed from their compliance with the FSDG, so it includes a variety of projects with different practical goals. Some are more experimental or hacker-oriented, while some are more specialized (like distributions for embedded devices). Trisquel aims to be very user-friendly, focusing on having strong accessibility features out of the box, a simple design, and good language support. Having a regular release cycle, Trisquel also aims to be a good choice for server infrastructure.

**LM:** Are free distros becoming more or less popular?

**RR:** I don't have specific statistics, as we don't track our users. Our server traffic indicates a steady interest in our project, and we have a quite active community participating in forums, mailing lists, and IRC.

**LM:** Describe the work involved in becoming FSDG-compliant.

**RR:** In addition to the cleanup of non-free components I mentioned, there are other requirements like not recommending proprietary software in the documentation and on community communication channels like forums and such. An important requirement is self-hosting: it is not enough to make a free installer (like a live image) for a distro that has non-free components in their repositories. Mainly, it focuses on the responsibility that comes from distributing software to others.

**LM:** Trisquel supports several desktops, such as MATE, LXDE, and Sugar, the desktop originally designed for the educational purposes by One Laptop per Child. Do any of the supported desktops involve special work?

**RR:** All of the desktops that we distribute as a live environment are quite polished, but the MATE desktop (our recommended default) is the one that takes the most work. MATE is a very good choice for accessibility, due to its good compatibility with screen readers and with keyboard navigation. Our target is that the system must be installable without help for people with disabilities including blindness. It is also a good choice for computers that have no 3D acceleration (which in many cases can only be achieved with non-free drivers), as it is an optional requirement for that desktop.

**LM:** What other features make Trisquel stand out?

**RR:** I've mentioned most of the practical advantages, as many stem from the project values in the first place. A goal that goes hand-in-hand with accessibility is the simple design and the ease of use for which we aim.

One thing that is remarkable is how easy it is to contribute improvements. We use quite simple Bash scripts (we call them package-helpers) to apply modifications to upstream packages, which get built and published for testing automatically through our CI infrastructure and then published for production after review.

**LM:** Do you have any stats on downloads, commits, and developers?

**RR:** We only track downloads partially, since there are many mirrors that we don't get statistics from. Our main site has counted over a million downloads. Our most active repository is the previously mentioned package-helpers, with over 2,000 commits affecting 300 + source packages. That project has gotten contributions from 25 developers. We also have volunteers helping with the documentation, translations, build systems, and other sub-projects.

**LM:** How is Trisquel governed? How are decisions made?

**RR:** Trisquel is established as a non-profit organization registered in Spain, which takes care of the legal and tax-required obligations. The project is quite horizontal in its structure, and we make most decisions during the developers' meetings I mentioned. In terms of community management, we are lucky to have a good amount of long-term participants in our forums and lists that are excellent at encouraging newcomers, keeping the conversation on track, and notifying moderators the few times intervention is needed.

**LM:** Who is the target audience for Trisquel?

**RR:** We try to make it as wide as possible. Trisquel is not a specialized distro. It is not particularly hacker-oriented, but you can dig into the code and technical details to any depth, so it can be used by people of very different levels of expertise. It targets both desktop and server users, and recently we added ARM and BOW POWER architecture support to expand on the possible use cases. Ultimately we want it to be a very flexible platform for people that are walking up the "freedom ladder" and are exploring and learning about free software.

**LM:** Are there any future plans?

**RR:** Our main goals at the moment are to find more developers and other contributors, to renew our www website, and to continue to grow our build infrastructure.

**LM:** Is there anything else readers should know about Trisquel?

**RR:** I invite people to try it out, check out our community, and explore the many projects we work on and that always need more contributors. Also, Trisquel is sustained 100 percent from donations from our community [7].

# Info

+   1. FSF free distributions: https://www.gnu.org/distros/free-distros.html
+   2. Trisquel: https://trisquel.info/
+   3. ubuntu-purge: https://gitlab.trisquel.org/trisquel/ubuntu-purge
+   4. Linux-libre: https://www.fsfla.org/ikiwiki/selibre/linux-libre/
+   5. FSDG: https://www.gnu.org/distros/free-system-distribution-guidelines.en.html
+   6. RYF: https://ryf.fsf.org/
+   7. Donations: trisquel.info/donate