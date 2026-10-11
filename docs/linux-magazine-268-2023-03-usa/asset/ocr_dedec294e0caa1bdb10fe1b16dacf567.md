# # NEWS

Kernel News

bias, the bug reports I've seen there are generally a waste of my time, and if I'm going to choose which users I'm going to help for \*free\*, it's going to be the one which is far less frustrating to me as the volunteer. \*100 times more popular\* is not necessarily a feature if what we get is 1000 times the noise.\"

Theodore further added, \"Artem, it seems to me that you are hoping that volunteers will provide a commercial level of support — and that's just never going to happen. The users vastly outnumber us developers by orders of magnitude, and [... ] we need to clearly express that any kind of support is best efforts only, and if someone has anything business\-, mission\-, or life-critical, they should darned well pay \$\$\$ for a proper support contract.\"

Linus Torvalds also came down – at least for the moment – on the side of preferring email over a web interface. When Artem remarked, \"I just want a bugzilla where I can CC \_any\_ developer if, and \_only if\_, they are willing to work within its confines. That's it.\" Linus then replied:

Guess what that \*add developer to the Cc\* is called? \*Email\*

What you do is fill in the bugzilla entry with all the data you want. Then you use email to inform people about it.

Put enough data in the email that the developer knows whether it's even worth looking at the bugzilla entry or not. Don't just put a link to the bugzilla. Most developers will just go 'oh, this looks like spam.' Put the overview in the email, enough information that the developer can go 'Ah, this is worth my time'\_, and\_ the link to bugzilla. That gives you exactly what you ask for: you can CC \_any\_ developer. And it

doesn't force the developer to have to go to some bugzilla web interface unless the developer thinks it actually adds value.

This is \*literally\* how I end up using bugzilla. As you say, I actually do end up looking at bugzilla entries in the end, but I only do it once it has hit my mailbox first, and I have some fairly good indication that it's worth my time to look at it.

And yes, for some projects and for some developers you can do that email integration from within bugzilla itself. That's how people reach me.

But this is exactly the kind of part of bugzilla that is a TOTAL HORROR-SHOW to manage, and it's impossible to expect every developer to be somebody that can be listed on bugzilla, without bugzilla becoming a prime way to send spam.

Which is why in the general case, you really should consider email to be the 'lingua franca' of kernel development communication. It doesn't have the fundamental limitations and management issues that bugzilla has. If you want to add more people to the Cc in an email, you just do it.

The discussion is not over by any means. I would expect the debate to be ongoing for years to come, in spite of Linus's stated preference. If Linus said something like, \"we will never use a web-based bug tracker,\" then the debate might end. But it's one of Linus's great features that he won't put a definitive end to a discussion unless he feels it is really truly true that one side is absolutely correct and the other absolutely wrong. He kept the revision control discussion going for years and years, until finally he had no choice but to implement a proper solution himself. I don't think he'll do the same for a bug tracking system, but we can hope.

###

###