# # NEWS

different people (as different bug reports) but usually the subsystem only engages with one to fix the issue. In the-ory bugzilla can mark the latter as dupe, but that requires someone to spend an enormous amount of time on evaluation and admin.

“That’s not to say we can’t improve our process, it’s just to set expectations that we’re never going to approach anywhere near a perfect bug process. Most of the improvements that worked so far involve having someone coach bug reporters through the process of either testing patches or reproducing the problem in a more generic environment . . . which I think most people would agree can’t really fall wholly on maintainers.”

At around this point, various developers did start to consider potential bug tracking solutions. One idea was to rely exclusively on email – simply track bugs via the mailing list, and use scripts or some other form of infrastructure to supplement that. In fact, Laurent Pinchart objected to this idea, saying that there really was no way to track the status of bug reports and fixes using email alone. But Thorsten replied, “I’d disagree partially with that, as my regression tracking bot ‘regzbot’ [...] does exactly does that: tracking, by connect the dots (e.g. monitoring replies to a report as well as recording when patches are posted or committed that link to the report using Link: tags), while making sure nothing important is forgotten. But sure, it’s still very rough and definitely not a full bug-tracker (my goal is/was to not create yet another one and needs quite a bit of hand holding from my side. And I only use it for regressions and not for bugs (on purpose).”

Laurent replied, “Patchwork does something similar for patches, and I agree that it would be possible to use e-mail to manage and track bug reports with tools on top (and don’t worry, I’m not asking for regzbot to be turned into a bug tracker :-)). It however has to rely on lots of heuristics at the moment, as the data we exchange over e-mail is free-formed and lacks structure. I’ve been dreaming of support for structured data in e-mails, but that’s a pipe dream really.”

Also, Laurent made another point, saying, “The huge elephant in the room is that most maintainers are overworked.

Whether a bug report arrives in my mailbox as an e-mail straight from the reporter or from a bug tracker will make very little difference if I don’t have time to look into it (I would even argue that bug trackers are even worse there: if I’m really short of time, I’m more likely to prioritize replying to e-mails instead of having to open a link in a web browser). As long as we don’t address the main-tainer bottleneck in the kernel, bug tracking will suffer.”

Artem, however, was strongly against an email-based solution. He said, “Debian uses an email based bug tracker and you know what? Most people avoid it like a plague. It’s a hell on earth to use. Ubuntu’s Launchpad which looks and feels like Bugzilla is a hundred times more popular.”

“To which Laurent replied sardonically, “It would be pretty sad if the only options we could come up with for bug tracking would be either popular with reporters and ignored by maintainers, or the other way around.”

Tony Luck defended a web-based approach, saying, “Web interfaces have the advantage that they can be full of boxes which indicate useful details to supply. Like what kernel version? Did this work on an older version, [if so, which one! Which CPU vendor/model are you using? Is there an error message? Are there warnings in the console log before the error? Can you upload a full console log? Does this happen repeatably? What are the steps to reproduce? Etc.etc. Sometimes it takes a few round trips by e-mail to establish the baseline facts.”

Slade Watkins agreed, saying, “Email – imo – is good for discussions, but not for reporting bugs. Web has upsides of being easier to navigate (sometimes faster) with just a few clicks/keyboard shortcuts and some words to describe an issue, steps to reproduce, kernel versions it affects, etc.”

On the flip side of the equation, Theodore Ts’o said, “Funny thing, I’ve largely given up on getting any kind of useful bug report from Launchpad, so I’ve largely ignored it. In contrast, the bug-reports I get for ext4profs from Debian are generally far more actionable, with bug reports that have all of the data so I can actually root cause the problem, and help the user.”

He added, “So Launchpad may be pretty, but perhaps because of selection