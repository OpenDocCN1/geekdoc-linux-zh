
Even to you, it is important to prepare for that day, just in case. Being prepared is more a matter of having the right procedures prepared and knowing what to do rather than deploying some technology. This is especially important, because in many cases, a successful intrusion can lead to an incredible state of confusion.

There is no “cookbook” on how to be prepared. However, guidelines have been established by the CERT, the Computer Emergency Response Team, on how to detect a break-in and report successful break-ins. These guidelines can be found at `ftp://ftp.cert.org/pub/tech_tips/intruder_detection_checklist`.

A group of the IETF is currently doing some similar work (`http://www.ietf.org/html.charters/grip-charter.html`).

And, there are documents available on how to recover from an intrusion at `ftp://info.cert.org/pub/tech_tips/root_compromise`.

Finally, a recommended lecture on how to handle and identify network probes can be found at `http://www.network-defense.com/papers/probes.html`.

Some sound advice is to prepare in advance, which should include identifying an incident response team in your organization to be responsible for responding to possible intrusions into your infrastructure. This team will verify intrusions, track problems, implement counter-measures, and communicate with your users. If you discover an intrusion, be sure to communicate your findings to both:

- CERT—The Computer Emergency Response Team (`http://www.cert.org`).
- FIRST—The Forum of Incident Response and Security Teams (`http://www.first.org/team-info`).

Communicating this information is important, because if your break-in is the first of its kind, the information you give to CERT and FIRST may help prevent the break-in from occurring in other places or help to track and apprehend the intruder.

## Summary

This chapter tried to give a background on security from an IT point of view. You should spend some time “surfing” the several URLs listed in this chapter. You also need to be aware that despite all the technologies that have been developed so far for protecting, preventing, and detecting, the war is just starting.

Initially, the opponent was an individual or small group using mainly a sequence of commands based on their knowledge and guesses to probe and penetrate. These same people have now developed tools (like nmap) to help them by automating some tasks like probing vulnerable hosts.

Unfortunately, what we are witnessing today is the emergence of a new generation of tools allowing an opponent to launch distributed denial of service (DDoS) using hundreds of machines (most of the time which have been compromised) in a coordinated way. More information on this new topic can be found at the following sites:

- http://www.fbi.gov/nipc/trinoo.htm.
- http://www.cert.org/advisories/CA-2000-01.html.

Even worse, it is strongly assumed that tools have been developed (and closely held by their authors) for automating the tasks of remotely compromising dozens of machines, exploiting security holes, and installing components of DDoS tools. However, there are currently no tools that allow a site to defend itself efficiently against DDoS attacks. Patching security holes in an IT system becomes a nightmare, since during the time a security bug is discovered, it becomes public knowledge and hundreds or thousands of machines can be compromised. Obviously, the risk is out there, and system administrators are in need of new tools—more intelligent tools that can be used for collaboration. And, above it all, there is a need more than ever to have CERT track opponents quickly and from an international perspective.

A system without users is like a racecar without a road. It looks nice, can go real fast, but really doesn’t serve much of a purpose, unless of course you like off-roading. From the previous chapters, you learned the techniques necessary to design, build, and maintain your computer infrastructure. However, while you’re probably proud of what you’ve created, and confident that the systems are stable and secure, eventually you will have to let the users take the system for a ride.

However, now that your shiny new racecar is prepared, you just do not want to hand over the keys and walk away, for if you do, you’ll turn around and find your car dented and scratched, and if you’re really unlucky, up on blocks with the hood open! Before you hand over the keys to your users, you’ll have to have a plan in place for granting access. Access to systems consists of providing an access ID and password, as well as defining other characteristics that form a user account.

Each account is special and identifies a unique entity on your computing system. Planning your account creation strategy in advance will help you manage both the users as well as the resources they access. Here are a few recommendations for an account creation strategy:
