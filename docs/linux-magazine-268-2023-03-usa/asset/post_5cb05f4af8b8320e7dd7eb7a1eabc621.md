
# NEWS

## Kernel News

Meanwhile, Konstantin Ryabitsev, a member of the Linux Foundation's infrastructure team, gave a summary from the perspective of that team:

*The bugzilla as a software platform is a Mozilla product, not Linux Foundation. Unfortunately, it's pretty much dead:*

1. all development has stopped years ago
2. it doesn't even work with recent MySQL servers
3. it is written in perl5 and can only pretty much run with mod_perl

'We're committed to running it as far as we can, but we all must also admit that the platform is near-death and probably will become an ever-increasing burden to keep it operating. Heck, one of our IT staff is currently trying to convert bugzilla.kernel.org to use Postgres just so we can keep operating it past the end of 2022.'

'The Linux Foundation IT is in charge of running infrastructure – we're not a development shop. All of our software projects are pretty much 'skunkworks'.'

He added that the Linux Foundation was potentially in a position to fund developers in some cases – but that this would require a very clear mandate from the community. Konstantin said, "Before we try to fix/replace bugzilla, we really need to figure out the entire process and pinpoint who is going to be the one in charge of bug reports. If you think that LF [Linux Foundation] should establish a fund for a position like that, then you should probably approach LF fellows (Greg KH, Shuah Khan), who can then talk to LF management. The IT team will be happy to support you with the tooling, but tooling should come second to that – otherwise we'll just be replacing an old and rusty dumpster on fire with a new and shiny dumpster on fire."

Artem suggested converting Bugzilla and all supporting systems to use GitLab instead. He said, "that will solve all the issues immediately." For one thing, he said, all patch committers would be automatically present, so they could be cc'd on bug reports. For another, the kernel source code directory tree could easily be split into separate components, and the relevant developers assigned to those components – again, ensuring they would be cc'd on bug reports.

Also, Artem added, "Linus, as a commander, may continue having his local git repo or using its own git website and get merge requests from gitlab.kernel.org. For him barely anything will change (aside from URLs to fetch from)."

But Greg slammed the door firmly on that idea, remarking, "For loads of reasons that have been stated before, we aren't going to move everything to gitlab, sorry. That's a non-starter for a wide range of reasons, not the least being one who is trying to solve a 'we have no one who wants to wrangle bugs in bugzilla' problem with 'move all of our code hosting infrastructure to a totally different thing that can't even provide the basic things that we have today.' Sorry, not going to happen, gitlab is not the solution here."

Konstantin also noted that with GitLab, "you will still have all the exact same problems as long as nobody is in charge of handling incoming bugs. There are plenty of active github/gitlab projects with thousands of open issues that nobody is working on for the exact same reason nobody is working on bugs filed via bugzilla – the right people didn't see it (or are actively ignoring it, because they are working on something else)."

In addition, Konstantin also reminded Artem, "Gitlab is also a commercial open-core project. It is permanently in danger of being swallowed by some $ENTITY_NOBODY_LIKES, who will for sure look to prioritize which kinds of things go in to the 'open core' part and what kinds of things are only available with subscription, in order to improve profit margins."

To which Artem replied, "That leaves us with Bugzilla that no one wants to touch and some people actively want to delete altogether. In other words, no central place to report bugs or keep track of them."

James Bottomley pointed out that there was no truly obvious fix for the situation. He said:

*The sad fact is that a lot of bug reports aren't actionable, meaning the reporter can't give a reproducer and also can't easily test patches[.] sometimes by luck the maintainers can work out what the issue is but a lot of the time they have no idea. Then there are tons of bug reports with responses like 'I think xxx commit fixes your problem, can you test it?' for which the conversation dies there. There's also the thundering herd problem: some bugs get reported by many different people (as different bug reports) but usually the subsystem only engages with one to fix the issue. In the-ory bugzilla can mark the latter as dupe, but that requires someone to spend an enormous amount of time on evaluation and admin.*

“That’s not to say we can’t improve our process, it’s just to set expectations that we’re never going to approach anywhere near a perfect bug process. Most of the improvements that worked so far involve having someone coach bug reporters through the process of either testing patches or reproducing the problem in a more generic environment . . . which I think most people would agree can’t really fall wholly on maintainers.”

At around this point, various developers did start to consider potential bug tracking solutions. One idea was to rely exclusively on email – simply track bugs via the mailing list, and use scripts or some other form of infrastructure to supplement that. In fact, Laurent Pinchart objected to this idea, saying that there really was no way to track the status of bug reports and fixes using email alone. But Thorsten replied, “I’d disagree partially with that, as my regression tracking bot ‘regzbot’ [...] does exactly that: tracking, by connect the dots (e.g. monitoring replies to a report as well as recording when patches are posted or committed that link to the report using Link: tags), while making sure nothing important is forgotten. But sure, it’s still very rough and definitely not a full bug-tracker (my goal is/was to not create yet another one and needs quite a bit of hand holding from my side. And I only use it for regressions and not for bugs (on purpose).”

Laurent replied, “Patchwork does something similar for patches, and I agree that it would be possible to use e-mail to manage and track bug reports with tools on top (and don’t worry, I’m not asking for regzbot to be turned into a bug tracker :-)). It however has to rely on lots of heuristics at the moment, as the data we exchange over e-mail is free-formed and lacks structure. I’ve been dreaming of support for structured data in e-mails, but that’s a pipe dream really.”

Also, Laurent made another point, saying, “The huge elephant in the room is that most maintainers are overworked. Whether a bug report arrives in my mailbox as an e-mail straight from the reporter or from a bug tracker will make very little difference if I don’t have time to look into it (I would even argue that bug trackers are even worse there: if I’m really short of time, I’m more likely to prioritize replying to e-mails instead of having to open a link in a web browser). As long as we don’t address the main-tainer bottleneck in the kernel, bug tracking will suffer.”

Artem, however, was strongly against an email-based solution. He said, “Debian uses an email based bug tracker and you know what? Most people avoid it like a plague. It’s a hell on earth to use. Ubuntu’s Launchpad which looks and feels like Bugzilla is a hundred times more popular.”

To which Laurent replied sardonically, “It would be pretty sad if the only options we could come up with for bug tracking would be either popular with reporters and ignored by maintainers, or the other way around.”

Tony Luck defended a web-based approach, saying, “Web interfaces have the advantage that they can be full of boxes which indicate useful details to supply. Like what kernel version? Did this work on an older version, [if so, which one]! Which CPU vendor/model are you using? Is there an error message? Are there warnings in the console log before the error? Can you upload a full console log? Does this happen repeatably? What are the steps to reproduce? Etc.etc. Sometimes it takes a few round trips by e-mail to establish the baseline facts.”

Slade Watkins agreed, saying, “Email – imo – is good for discussions, but not for reporting bugs. Web has upsides of being easier to navigate (sometimes faster) with just a few clicks/keyboard shortcuts and some words to describe an issue, steps to reproduce, kernel versions it affects, etc.”

On the flip side of the equation, Theodore Ts’o said, “Funny thing, I’ve largely given up on getting any kind of useful bug report from Launchpad, so I’ve largely ignored it. In contrast, the bug-reports I get for ext4profs from Debian are generally far more actionable, with bug reports that have all of the data so I can actually root cause the problem, and help the user.”

He added, “So Launchpad may be pretty, but perhaps because of selection
