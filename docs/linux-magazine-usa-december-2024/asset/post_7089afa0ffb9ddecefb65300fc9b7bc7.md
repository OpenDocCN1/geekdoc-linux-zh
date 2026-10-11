
## Kernel News

that bcachefs is _definitely_ more trustworthy than btrfs, in terms of ‘will this filesystem ever go unrecoverable or lose my data’ – I’ve seen many reports of people who’ve put it through the same situations where btrfs [fails]. I’ve even seen people compare bcachefs’s robustness in positive terms vs. .fs/x/, and that’s the result of a *hell* of a lot of work with the #1 goal of having a robust filesystem that _never_ loses data.”

Although in the next breath, he did add a public disclaimer: “Please don’t rush out and switch to bcachefs just yet. I still have a backlog of bugs and issues – some of them serious, as in your filesystem will go emergency read only – and I don’t want people getting bit. There’s still a ton to do; I’m not taking EXPERIMENTAL off until at least the fuzz testing for on disk corruption is in play.”

Kent also defended his work ethic and development practices, saying, “Look, I’ve been doing this for a long time, I’ve had people running my code in production for a long time, and I’m working with my users on a daily basis to address issues. I don’t throw code over the wall; I do everything I can to support it and make sure it’s working well.” He added, “when I ship code, I’m _always_ weighing ‘how much do we want this’ vs. ‘risk of regression/ risk in general’ – I’m not just throwing out whatever I feel like.”

Kent went on to say, “Look, this is the filesystem you’re all going to want to be running in – knock on wood – just a year or two, because I’m working to make it more robust and reliable than xfs and ext4 (and yes, it will be).”

However, in terms of bcachefs’s reliability, Linus replied plainly:

> “I’ll believe that when there are major distros that use it and you have lots of varied use.

> “But it doesn’t even change the issue: you aren’t fixing a regression, you are doing new development to fix some old problem, and now you are literally editing non-bcachefs files too. “Enough is enough.”

This attitude seemed to perplex Kent. He replied:

> “What is to be gained by holding back fixes, if we’ve got every reason to believe that the fixes are solid?”

> “And yes, these _are_ solid, the rhash table stuff was done months ago (minus the deadlock fix, that’s more recent), the re_run_pending stuff was mostly done months ago as well, and _heavily_ tested (including using it as replacement backend for kfree_rcu, which is the eventual goal there).”

> “And the genrad code is code that I also wrote and maintain, and those are simple patches.”

> “To which Linus merely quipped, “What is to be gained by having release rules and a stable development environment? I wonder.”

> “Linus then replied to his own quip a few minutes later, saying: “But seriously – thinking that ‘I changed a thousand lines, there’s no way that introduces new bugs’ is the kind of thinking that I DO NOT WANT TO HEAR from a maintainer.”

> “What planet ARE you from? Stop being obfuscating.”

> “Kent replied, “I’m not sending you anything here that isn’t a fix for a real issue.”

At this point, stepping back for a moment, Linus offered a more thorough explanation of his thinking:

> “Kenton, bugs happen. The number of bugs that happen in ‘bug fixes’ is in fact quite high. You should see the stable tree discussions when people get heated about the regressions introduced by fixes.”

> “This is, for example, why stable has the rule of fixes being small (which does get violated, but it is at least a goal: it cannot be bigger than 100 lines, with context), because small fixes are easier to think about and hopefully they have fewer problems of their own.

> “It’s also why my ‘development happens before the merge window’ rule exists. “If you have to do development to fix an old problem, it’s for the next merge window. Exactly because new bugs happen. We want stability.”

> “The fixes after the merge window are supposed to be fixes for regressions, not ‘oh, I noticed a long-standing problem, and now I’m fixing that’."

> “But obviously the same kind of logic as for stable trees apply: if it’s a small obvious fix that would be stable material *anyway*, then there is no reason to wait for the next release and then just put it in the stable pile.

“So I do end up taking small fixes, because at that point it is indeed a ‘it wouldn’t help to wait’ situation.”

“But your pull requests haven’t been *small fixes*. And I admit, I’ve let it slide. You never saw the last pull request, when I sighed, did a ‘git fetch’, and went through every commit just to see. And then did the pull for real.

“This time I did the same. And came to the conclusion that no, this was not a series of small fixes any more.”

To Linus’s ‘bugs happen’ comment, Kent replied:

“I _.know_.”

“Look, filesystem development is as high stakes as it gets. Normal kernel development, you fuck up – you crash the machine, you lose some work, you reboot, people are annoyed but generally it’s ok.

“In filesystem land, you can corrupt data and not find out about it until weeks later, or _worse_. I’ve got stories to give people literal nightmares. Hell, that stuff has fueled my own nightmares for years. You know how much grey my beard has now?

“Which is why I have spent many years of my life building a codespace and development process where I can work productively where I can not just catch but recover from pretty much any fuckup imaginable.

“Because peace of mind is priceless…”

At this point in the conversation, Carl E. Thompson joined in, trying to bridge the gap. He said:

“Kent, I’m not a kernel developer I’m just a user that is impressed with backefs, uses it on his personal systems, and eagerly waits for new features. I am one of the users who’s been using backefs for years and has never lost any data using it.

“However I am going to be blunt: as someone who designs and builds Linux-based storage servers (well, I used to) as part of their job I would never, ever consider using backefs professionally as it is now and the way it appears to be developed currently. It is simply too much changed too fast without any separation between what is currently stable and working for customers and new development. Your work is excellent but ‘process’ is equally and sometimes even more important. Some of the other hats I’ve worn professionally include as a lead C/C++ developer and as a product release manager so I’ve learned from very painful experience that large projects absolutely *must* have strict rules for process. I’m sure you realize that. Linus is not being a jerk about this. Just a couple of months ago Linus had to tell you the exact same thing he’s telling you again here. And that wasn’t the first time. In your plan to just continue to break the rules and do whatever the heck you want until Linus stops bothering you! I don’t think that’s a good plan.

“Since I’m already being blunt I’m going to be even more blunt: You have a serious problem working with others. In the past and in this thread I’ve read where you seem to imply that other kernel developers are gatekeeping and resist some of your ideas because you’ve created something that (in your opinion) is already better in some ways than some of things they’ve created. But from where I’m sitting the problems you’ve experienced are 90% because of ‘you’. You’re an adult and you need to understand that about yourself so you can do something about it.”

Kent got the final word of the conversation, replying:

“Your guys are freaked out because I’m moving quickly and you don’t have visibility into my own internal process, that’s all.

“I’ve got a test [cluster], a community testing my code before I send it to Linus, and a codespace that I own and know like the back of my hand that’s stuffed with assertions. And, the changes in question are algorithmically fairly simple and things that I have excellent test coverage for. These are all factors that let me say, with confidence, that there really aren’t any bugs in this this pull request.

“Look, there will always be a natural tension between ‘strict rules and processes” vs. ‘weighing the situations and using your judgement’. There isn’t a right or wrong answer as to where on the spectrum we should be, we just all have to use our brains.

“No one is being perfect here, Linus and I are just sitting in different places with different perspectives. He has a responsibility as someone managing a huge project to enforce rules to see best, while I have a responsibility to support users with working code, and to do that to the best of my abilities.”

The discussion ended there. My own take on the situation is that Linus generally prefers to win an argument rather than enforce his position. He may have a reputation for being mean and bombastic, but I believe that looking only at those snapshots tends to miss what’s really going on. In general, Linus loses patience when he feels the other person has had something clearly explained and is willingly refusing to get the point.

So, since Kent seems to be honestly disagreeing with Linus in this conversation, I think it could go either way. I wouldn’t be surprised if Linus, for example, accepts another big patch from Kent and gives him another reminder that this needs to change. At the same time, in this discussion, Linus did say “enough is enough”, and that generally indicates that he’s about to enforce the rules. To me, it really could go either way at this point.

Part of the problem is that many kernel developers are really amazing, and there can be a certain amount of arrogance that goes along with having such amazing skills and abilities. Kent would not be the first Linux developer to feel that their contributions were better and more carefully written than other people’s and deserving of special treatment. Part of Linus’s main discovery of the principles of open source development was to encourage people in their contributions. In the spirit of fun, I will say, if Linus turned developers away simply because they were arrogant, he might have run out of contributors a long time ago. ■■
