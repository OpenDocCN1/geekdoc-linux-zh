
## Pidora

One of the newest Pi distros is based on the popular Fedora. Is it the best choice?

There was a spin of Fedora for the Raspberry Pi during the early days of Pi release, but that was quickly dropped in favour of Raspbian when it proved to be a bit slow and buggy. It was almost two years after this incident that a proper version of Fedora was released on the Raspberry Pi in the form of Pidora. An almost straight-up port of the codebase to the specific ARM architecture of the Pi, Pidora has had a few tweaks to let it run on Pi hardware without much loss in performance, at least.

The very first thing to note is that the problems of Fedora on the Pi in the past are long gone. This is a very mature operating system that is stable and generally runs well on the Raspberry Pi. In terms of speed, it’s not as fast as Raspbian or Arch Linux and in the case of Raspbian this may be due to a number of factors. Pidora uses Xfce, for one, which is known to be a little heavier than the LXDE that Raspbian uses. Fedora also uses much newer software that is somewhat designed to be run on computers which are slightly more high-end, while Raspbian is based on an older version of Debian with more lenient software. It was the biggest difference but it all adds up with the other problems.

Booting from NOOBS is painfully slow and prone to errors – something that doesn’t occur with Raspbian or the other distros on NOOBS. Installing straight from the image removes this problem but, unfortunately, Pidora has one other disadvantage over Raspbian: lack of software.

![](img/c7d3278283754436651c50a2e9c72912_73_0.png)

Pidora is more mature than the version of Fedora on the Pi from last year

More software is being added all the time but a lot of basic or useful yet obscure packages available for Raspbian just aren’t in the repository. The essentials are there and there are plenty of programming choices, but combine this with a lack of official Pi accessory support and it becomes less attractive for project work.

It’s definitely not a bad distro, though. If it had ended up being the default when the Pi launched then we’d likely be saying similar things about Raspbian. However, there’s very little reason to use it over its Raspbian counterpart.

> “A lot of basic or useful yet obscure packages just aren’t in the repository”

![](img/c7d3278283754436651c50a2e9c72912_73_1.png)

Other operating systems are faster but at least Pidora is stable enough

### SCORES

| Category | Description | Score |
| :--- | :--- | :--- |
| Updates | Pidora is kept up date for the moment, however there’s no guarantee it will stay this way | 7 |
| Useability | The installation is superior to Raspbian’s and Xfce is a more useable desktop | 9 |
| Educational tools | You can easily program on Pidora but there are no specific tools to aid in learning it | 3 |
| Flexibility | As flexible as any Fedora distro but limited by its package choices and lack of Pi accessory support | 6 |
| Overall | We do really like Pidora but for everything you’d want to use a Raspberry Pi for, Raspbian or Arch is just better. | 6 |

## RISC OS

### The Acorn Computers OS keeps on going and keeps on being updated

The last time we did a PI OS group test we slightly enjoyed the blast from the past that was RISC OS, remembering our time in school using Acorn Computers that our Tesco Computers for Schools vouchers paid for. We came away realising that the tint on our rose glasses was a bit strong and struggling to get any screenshots off the SD card.

Since then, RISC OS has been updated a few times, increasing the amount of available software, improving the performance of the OS and finally letting us easily export PNG screenshots for this article. It's still very much the same RISC OS though, a curious novelty from another time that doesn't really fit in with the ecosystems of modern operating systems.

While RISC OS is not Linux it does have a similar file structure and uses a package manager, but otherwise it is completely its own thing. Using RISC is different from other operating systems as it uses a three-button system for clicking and opening menus, unlike the two-button standard of today. This can be confusing for new users, along with the way apps open on the desktop and the way they don't always require double-clicks to launch. When it is in a full-screen window, it covers the panel and a whole host of other quirks. If you're used to the traditional desktop metaphor there are a lot of new workflow processes to get your head around for something you're unlikely to use as your main computer.

![](img/c7d3278283754436651c50a2e9c72912_74_0.png)

Diving into RISC OS is like time travelling back to three decades ago

As for teaching tools there are very few. You won't really be learning to code on here unless you like using BASIC or already have a bit of knowledge in Perl or C. You can access the GPIO port but it's not very well suited for all projects; Raspbian and Arch would be better.

Things have changed in the 18 months since we first checked out RISC OS on Pi, but it's either not enough or it's just never going to go in the direction of Raspbian. It's definitely interesting, though, so if you have a few hours to play with it then we recommend giving it a shot.

![](img/c7d3278283754436651c50a2e9c72912_74_1.png)

There are a lot of different systems and processes to get your head around

> “While RISC OS is not Linux, it does have a similar file structure”

| Category | Comments | Score |
| :--- | :--- | :--- |
| **Updates** | Surprisingly, RISC OS is kept well up to date for a distro we can only imagine is not very popular | 6 |
| **Usability** | RISC is fine to use but it's just that little bit different to what a lot of people are accustomed to | 6 |
| **Educational tools** | Basically none are included with RISC OS and nothing can really be installed for this | 2 |
| **Flexibility** | With some perseverance and know-how you can use it for a few projects but less than others | 3 |
| **Overall** | RISC OS is a very different operating system to the others on this test, which isn't a bad thing but it is not conducive to education | 4 |

## Arch Linux

### Not quite Linux from scratch, but near enough as Ras Pi operating systems go

For just about as long as there's been a Raspbian distro on the Raspberry Pi Foundation's site there's also been an Arch alternative for those a little more adventurous in their choice of operating system.

Raspbian gets you going straight away with an excellent selection of apps. Arch provides users with a command-line interface and only a bare smattering of extra packages over the Linux kernel to make it work.

Arch has the bare essentials available to be built upon for a perfectly customised distro. To that end, this version comes with the pacman command line package manager to help you install any available software from the repository including desktops, media players and others. It enables you to have no bloat on the system and the correct setup will always be faster than a modified Raspbian for a lot of projects or applications.

![](img/c7d3278283754436651c50a2e9c72912_75_0.png)

Arch Linux isn't clunky, it has the bare necessities available for full customisation

As for Ras Pi-specific functions, it does quite well in this regard too. The Pi camera board is supported and so are the GPIO pins – the latter allowing access to a huge number of Pi accessories, including Adafruit screens and sensors and other physical devices. Some of it can be trickier to use, as you can't rely on pre-built Raspbian software, but it is doable with some of the more complex additions.

For normal users, though, it can be quite terrifying. All knowledge is assumed and, while you can easily find some quick tutorials to get started, it can be quite daunting. Even adding the Pi camera software takes a lot more effort than enabling it in the config menu. It does offer a unique opportunity to learn the intricacies of Linux, at least – which does keep in line with the Raspberry Pi education ethos – but there are a lot of one-off commands that might get lost in the process of getting it from zero to desktop.

> “While you can easily find quick tutorials to get started, it can be daunting”

For extremely custom projects you may well be better off using Arch over Raspbian. However, for a lot of users there won't be much of a difference in performance.

![](img/c7d3278283754436651c50a2e9c72912_75_1.png)

Be careful with one-off commands as they can easily get lost in the many processes

### SCORES

| | Description | Score |
|---|---|---|
| Updates | As a rolling release that is heavily tied to the Raspberry Pi, Arch gets a lot of updates | 8 |
| Usability | It's difficult to get into unless you're well versed in the ways of Linux | 4 |
| Educational tools | Using Arch is educational in itself, but it's more further education than a beginner's guide | 7 |
| Flexibility | About as customisable as it can be thanks to being built from almost scratch | 9 |
| Overall | Arch is excellent in its own way but it's definitely not for everyone and really not the best distro for something like the Raspberry Pi | 7 |
