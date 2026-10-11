
## Clem’s perfect laptop

In recent months, Clem Lefebvre has mentioned a possibility of a hardware “partnership and the manufacturing of Linux Mint laptops” but that hasn’t materialised yet, so we asked him what his idea of the perfect Mint laptop or Mint box was.

“Well, it depends for who. For many people the perfect laptop is cheap and has high specifications. [...] For me, the price doesn’t matter much and the perfect laptop is an object I enjoy manipulating, with a keyboard and a screen I love working with. I enjoyed the Sony TZXP for a long time and at the moment I like working on the Apple MacBook Pro,” Lefebvre says that Linux Mint doesn’t make money on partnerships, or at least not much money. “It’s not really part of our business model. We’re not a manufacturer, it’s not what we like doing and it’s probably not something we’d be good at. If we wanted to make money with laptops, we’d brand a cheap mass-produced laptop, something you could buy anywhere else.”

However, Lefebvre is ecstatic about the work Linux Mint has done with Compulab on the MintBox (see p31): “These units are unique: we’ll remember them all our life with pride as achievements.” Even if the margin on the Compulab boxes is low, it’s not been about the money for Lefebvre, it’s simply something he is thoroughly enjoyed doing. And in terms of whether they’ll ever manage to make their own laptops, he seems both a little wistful and aspirational on the subject: “If we do one day, they’ll probably be very special, very exciting, and I hope they’ll be pretty unique too.”

![](img/fb76008333fb7aef815b136f9f1afe5f_12_0.png)

Above: The Mint development team worked with Compulab on a series of tiny PCs. The fanless MintBox mini PC is the smallest at 10.8cm long.

He decided to focus on that project and to keep making it better with every new release. It has grown over since and although the goal never really changed, I think the principles behind it have remained the same.

## Has the vision for Mint changed in its over ten years of existence?

The mission is the same. In 2006, although it could definitely be improved for novice users, I strongly believed Linux was already the best desktop operating system for many of us. Ubuntu was the best distribution, so by adding improvements to it my main goal was simply to do better and better with each new release. This is still true today: we’ve focused on ourselves, on what we want to achieve and what people need, and our primary goal is to always publish a better release.

One key principle is for things to work out of the box. Whether you’re a novice or an experienced user, everybody likes features to just work. If you have to tinker with something to make it work, it should either be fixed or removed.

Another key principle is that you, the user, are central and nothing is more important than your user experience. When it runs on your computer, Linux Mint isn’t ‘our’ operating system; it’s yours. It needs to work for you.

> When it runs on your computer, Linux Mint isn’t ‘our’ operating system, it’s yours. It needs to work for you

Of course, free software and licensing is important to us, and so are other philosophical aspects, but, unlike a few other distributions, pragmatism is key. We’re not here to lecture anyone: our primary goal is to empower our users.

## You spoke out against some Linux distros spreading fear, uncertainty and doubt (FUD) about Linux Mint last year. How’s your FUD quota these days?

I’ve no time or patience for it and I tell my team not to react to it. Although FUD aims at harming your reputation, it usually has the opposite effect and contributes to a project’s growth. First, once people understand what’s going on they show a lot of support and actively start to deter it. Second, it makes a lot of people react and, all of a sudden everybody’s talking about you, even outside the Linux community and the audience you would normally reach. We’ve seen significant increases in growth with each large FUD campaign that has hit us.

Now, with that said, it’s also an issue for us of course because it’s a huge motivational blow. [...] FUD hits and reminds us how dark, nasty and bored some people are. [...] When we see FUD, our priority is to ignore it. What’s most at risk is a loss of motivation or a waste of time, two of the most essential resources needed during each development cycle. We only react to FUD when we really need to, and on these rare occasions we make sure to name and shame people who helped to spread it.

**Do you think the popular Linux distros are starting to build too many walls between each other?**

No, I don’t think so. The only thing I’m a bit worried about lately is Snap. I don’t think it’s okay for distributions to rely on an underlying Ubuntu Store. I’m also worried to see it disappear overnight. [...] Other than that, I don’t really see it that way.

## Forks & Crosses

Linux Mint's X-Apps are forks of GNOME apps (see Philosophy Of X-apps, below)

![](img/fb76008333fb7aef815b136f9f1afe5f_13_0.png)

Note: the text editor, Xed, is a fork of MATE’s pluma, which is in turn a fork of Gedit 2.

Standards are definitely imposed by momentum more than consensus these days, but I can’t complain about the quality of the end products and I’m quite happy to see more and more technology being common and adopted by a vast majority of distributions. A lot of this is coming from GNOME and Fedora developers and I for one enjoy it. GNOME itself is becoming more and more a product and its components fit less and less outside of its own environment. That’s an issue for other projects (which X-App partially solves, see left), but it’s also an improvement for GNOME itself and a great inspiration for others.

On our side, we’re developing more and more cross-distribution projects. It helps everybody. It helps other distributions of course, but it also helps our projects gain momentum, bug reports, pull requests and better quality overall. Whether it’s Cinnamon, X-Apps, the new Slack greeter, Blueberry… most of what we do is used by others and developers of these other distributions play a part in making these projects more successful.

**What’s the thinking behind the Spices website for applets, desklets and themes?**

Spices are add-ons for Cinnamon: applets (which are little components placed in your panel), desklets (which are little components placed on your desktop) themes (which change the look of Cinnamon) and extensions (which change the way Cinnamon works). You can install Spices from within the System Settings, but we need a website for people to be able to post comment and ‘like’ Spices. The more a Spice is liked, the higher its score is and the higher in the list Cinnamon users see it.

We asked Clem to explain the approach behind the development of X-Apps, a project for developing generic applications for GTK desktop environments:

> “The idea behind the X-App project is to develop a common set of libraries, tools and applications which work really well – not only for a particular desktop environment, but for all of them.”

Given that Linux Mint supports four desktops (three of which are based on GTK: Cinnamon, MATE and Xfce) and each environment is quite different, the X-App project enables Mint to move away from reliance on GNOME applications as it is focused on integrating well with GNOME Shell and sticking to user interface guidelines specific to GNOME.

There are also other benefits to this approach: “X-App is also cross-distribution so it gains momentum outside of Linux Mint,” says Clem. “From a development point of view, this allows the Linux Mint team to work on improvements and new features which reach a much larger audience than if it only targeted a single desktop or a single edition.”

**Have you considered a pay-what-you-want-model for the third-party Spices, like in Elementary OS?**

No. First, I’m not sure this would work for Spices. They’re open source implementations working against our APIs, in JavaScript. Second, we distribute them ourselves via a process which includes code reviews on GitHub. Second, I’m not keen on mixing commercial aspects and development. Our model is to distribute software for free and to attract developers who are passionate about what they do. We work with people who are having fun and whose motivation isn’t commercial. We don’t do bounties, we don’t let donations orientate design and everywhere we deal with money we make sure it doesn’t interfere with our relationships and the way our developers work. Even the way we ‘pay’ developers is designed so that there is no direct relationship between what they do and the money they receive. We don’t want money to dictate or even have an impact on what we want worked on; we want it to happen because developers want it done or because of a team decision.

**Have you had any user suggestions that have made it as features that surprised you at the time?**

Yes, of course. All the time in every single development cycle. There hasn’t been any release which shipped ‘exactly’ the set of features we had planned. We often postpone parts of what is planned and which isn’t ready at the end of the development cycle (we’ve a long backlog of great ideas yet to implement), and we also include implementations and new features which just landed during the cycle and came out of nowhere. It happens all the time… somebody says something.

## Philosophy of X-apps

![](img/fb76008333fb7aef815b136f9f1afe5f_13_1.png)

Above: Xviewer was forked from Eye of GNOME and is rapidly developing. In 18.2, its toolbar has been redesigned and now supports dark themes.
