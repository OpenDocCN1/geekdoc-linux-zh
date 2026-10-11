that bcachefs is _definitely_ more trustworthy than btrfs, in terms of ‘will this filesystem ever go unrecoverable or lose my data’ – I’ve seen many reports of people who’ve put it through the same situations where btrfs [fails]. I’ve even seen people compare bcachefs’s robustness in positive terms vs. .fs/x/, and that’s the result of a * hell* of a lot of work with the #1 goal of having a robust filesystem that _never_ loses data.”

Although in the next breath, he did add a public disclaimer: “Please don’t rush out and switch to bcachefs just yet. I still have a backlog of bugs and issues – some of them serious, as in your filesystem will go emergency read only – and I don’t want people getting bit. There’s still a ton to do; I’m not taking EXPERIMENTAL off until at least the fuzz testing for on disk corruption is in play.”

Kent also defended his work ethic and development practices, saying, “Look, I’ve been doing this for a long time, I’ve had people running my code in production for a long time, and I’m working with my users on a daily basis to address issues. I don’t throw code over the wall; I do everything I can to support it and make sure it’s working well.” He added, “when I ship code, I’m _always_ weighing ‘how much do we want this’ vs. ‘risk of regression/ risk in general’ – I’m not just throwing out whatever I feel like.”

Kent went on to say, “Look, this is the filesystem you’re all going to want to be running in – knock on wood – just a year or two, because I’m working to make it more robust and reliable than xfs and ext4 (and yes, it will be).”

However, in terms of bcachefs’s reliability, Linus replied plainly:

> “I’ll believe that when there are major distros that use it and you have lots of varied use.

> “But it doesn’t even change the issue: you aren’t fixing a regression, you are doing new development to fix some old problem, and now you are literally editing non-bcachefs files too. “Enough is enough.”

This attitude seemed to perplex Kent. He replied:

> “What is to be gained by holding back fixes, if we’ve got every reason to believe that the fixes are solid?"”

> “And yes, these _are_ solid, the rhash table stuff was done months ago (minus the deadlock fix, that’s more re-cent), the re_run_pending stuff was mostly done months ago as well, and _heavily_ tested (including using it as replacement backend for kfree_rcu, which is the eventual goal there)."”

> “And the genrad code is code that I also wrote and maintain, and those are simple patches.”

> “To which Linus merely quipped, “What is to be gained by having release rules and a stable development environment? I wonder.”

> “Linus then replied to his own quip a few minutes later, saying: “But seriously – thinking that ‘I changed a thousand lines, there’s no way that introduces new bugs’ is the kind of thinking that I DO NOT WANT TO HEAR from a maintainer.”

> “What planet ARE you from? Stop being obfuscating.”

> “Kent replied, “I’m not sending you anything here that isn’t a fix for a real issue.”

At this point, stepping back for a moment, Linus offered a more thorough explanation of his thinking:

> “Kenton, bugs happen. The number of bugs that happen in ‘bug fixes’ is in fact quite high. You should see the stable tree discussions when people get heated about the regressions introduced by fixes.”

> “This is, for example, why stable has the rule of fixes being small (which does get violated, but it is at least a goal: it cannot be bigger than 100 lines, with context), because small fixes are easier to think about and hopefully they have fewer problems of their own.

> “It’s also why my ‘development happens before the merge window’ rule exists. “If you have to do development to fix an old problem, it’s for the next merge window. Exactly because new bugs happen. We want stability.”

> “The fixes after the merge window are supposed to be fixes for regressions, not ‘oh, I noticed a long-standing problem, and now I’m fixing that’. "”

> “But obviously the same kind of logic as for stable trees apply: if it’s a small obvious fix that would be stable material *anyway*, then there is no reason to wait for the next release and then just put it in the stable pile.