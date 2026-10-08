
The profile directory will be something like `zx9rh0kQ.default`. It’s a good idea to move this rather than immediately delete it, and it’s probably a good idea to backup your bookmarks and make sure you know any saved passwords (or, better, make sure you saved in a password manager), because this information is all stored in the profile directory. Cookies are also stored here, so any website preferences will be lost too. Let’s move the profile directory to our home directory:

```bash
mv ~/.mozilla/firefox/zx9rh0kQ.default ~/OldProfile
```

Now restart Firefox and see what life with a virgin profile is like. For Chromium, the default profile directory is `~/.config/chromium/Default` (or `chrome/Default` if you’re using Google Chrome). You can check this is indeed where the active profile is stored by visiting `chrome://version`. Substitute this directory in the command above to have a clean Chromium profile.

If you’re using Firefox Sync, or have your Chromium profile synced to a Google account, then bookmarks, extensions and passwords are synchronized automatically. This is useful, but in the unlikely event a rogue extension is degrading your browsing experience, using this feature may well re-animate the problem. So do try things without syncing first. If this solves your problem and everything works, then you should:

```bash
$ rm -rf ~/OldProfile
```

because it contains encrypted passwords (and potentially payment information if you use that feature), as well as the keys by which a knowledgeable attacker can decrypt them.

While everyone wishes it wasn’t the case, it’s always possible that just by visiting a web page you can contract some kind of malware – without so much as clicking, downloading or running anything. Browser developers go to extraordinary lengths to preclude this outcome, and in fact they do a marvellous job because this kind of malware (unless you’re running outdated software) is extremely rare.

For it to gain a foothold, there would need to be a vulnerability in the browser, perhaps in a font or image rendering library. Or perhaps a pop-up is able to render in some way that hides a malicious download behind the close button. Generally speaking, an unpatched vulnerability that allowed arbitrary code execution straight from the browser would be quite high-value, so unless you’re someone like an activist, political dissident or darkweb mastermind that people with considerable hacking resources (governments, nation states, other darkweb masterminds) are very interested in, then you’re probably fine. After all, who would such a group risk losing their 0-day edge on a cavity?

Besides privacy concerns around using your tracking cookies (which isn’t the focus of this article), advertising networks have in the past been used to spread malware, by injecting malicious JavaScript or Flash applets. There’s no reason for the latter to be a problem now: Flash is all but dead and should be uninstalled. Chromium comes with its own PPAPI Flash plug-in which is heavily sandboxed, and by default should prompt before launching. Check this by visiting Settings > Privacy and Security > Site settings > Flash. By all means disable it outright if you want to be sure.

![](img/7a0a282248f9658f0c87e55744c797b6_84_0.png)

Note you can’t run Docker inside Firefox just yet, but account containers can — to quote Wu Tang Clan — protect ya neck.

## BROWSER EXTENSIONS TO USE

All this talk of extensions gone rogue might compel you to get rid of them altogether, but please don’t. Some of them are great, and some of them can really help you. For random web browsing, we unreservedly recommend some sort of ad (don’t tell management!–Ed) blocker. We favour uBlock Origin, but AdBlock Plus (which out of the box will provide a smoother browsing experience without breaking popular sites) is popular too. A close second on the essential extensions list is the EFF’s HTTPS Everywhere, which enforces HTTPS transfers, preserving privacy and preventing prying eyes from pilfering passwords. For extreme browsing security, NoScript (for Mozilla browsers) is your friend. This banishes JavaScript everywhere, allowing you to whitelist it piece by piece, or domain by domain. This is bundled with the Tor Browser, which is used by exactly the kind of people that repressive regimes target with malware.

Beware though, a lot of sites will behave unpredictably with this NoScript enabled. In particular, it can confuse payment processors, which might leave you staring at a blank page wondering whether or not you were charged. You probably weren’t, but the uncertainty isn’t worth it — be sure to disable it before attempting to part with your pennies, such as subscribing to Linux Format. For instance.

![](img/7a0a282248f9658f0c87e55744c797b6_84_1.png)

Extensions can frustrate your browsing experience, but these ones are awesome.

## Vulnerabilities and exploits

Malware begins with breaking programs and ends in tears. Find out how we rein it in.

Without some knowledge of memory management, pointers and execution stacks, it's hard to give a rigorous account of how programs get compromised and thus enable malware to do its thing. This isn't the time or place for such an in-depth look, but we can at least provide an only slightly hand-wave account of one way a program might be exploited.

Programs work with input, which might come from a user, a website, another program, a piece of hardware (like a keyboard or a sensor) or a file. For a program to work correctly, that input has to be correctly formed. If it's not, then it won't fit nicely into the memory allocated to it, and horrible things can happen. We'll be more specific about what those horrible things are in a moment, so bear with us. So, some kind of input validation ought to take place. If it does not, then the program will attempt to digest something that is the wrong size or shape for the memory assigned to it. As you can imagine, the results of this unpredictability can be unpredictable; to labour a metaphor, you may witness the digital equivalent of anywhere between regurgitation and a food coma. This might be application crashes or system slow-downs.

But it could be much worse. Once such a vulnerability is discovered, it can be exploited by specially crafting our malicious input. In extremis, instead of crashing a program by feeding it the wrong kind of cat GIF, we could have it execute the payload of our choosing, which might be a covert keylogger or a persistent backdoor to the host machine. Thus is the progression from vulnerability to exploitation to what is commonly referred to as malware.

For example, if we have a program that asks a user for a number and then spits out the square of that number, we first check that the raw input resembles an integer. If it doesn't, the program quits with an error (we could check for decimal input and coerce that to an integer too, but let's keep it simple). Compilers are fuzzy about data types, and the largest signed integer 64-bit registers can store natively is $2^{63}-1$, so we also need to check if an integer is too big (or negative and thus too small) - and if it is, bail with a different error.

There's more than meets the eye to these checks, since the raw input has to exist in some sort of buffer before it can be checked, and how can we know a priori how big to make that buffer? Let's not concern ourselves with that - smaller people than us have mostly figured it out. So at this stage we're sure we have an integer, and we want to make our computer square it. That's easy, except for the small (actually large) catch that the result of this squaring this integer could well be larger than the space we allocate for it. Multiplying an integer with itself will always give a positive integer, so we could use an unsigned int to store our result. That will work fine so long as that result is less than $2^{64}-1$, or, by some elementary mathematical deduction, our original input was less than $2^{32}$. If not, the result may spill into other memory, overwriting it. This so-called integer

### CVEs, BUGS AND BOUNTIES

There are good ways and bad ways to go about reporting newly discovered vulnerabilities. Up until they're disclosed to the relevant vendor or project, these are known as zero-day bugs. Day Zero being the day that disclosure happens. If you were in possession of a Zero Day, you could brag about it on Twitter (and publish full details on some medium that allows more than 280 characters) - sending affected parties, especially the relevant project, into a panic and possibly unleashing a wave of script-kiddie attacks.

Better yet be responsibly disclose the vulnerability privately, so that a fix can be rolled out before things get out of control. Some projects even operate a bug bounty program so that such efforts can be rewarded. Vulnerabilities are assigned an ID on Mitre's Common Vulnerabilities and Exposures (CVE) list, and once a suitable patch is in place, will provide public details of the vulnerability at https://cve.mitre.org. This will be picked up and packaged as a matter of urgency by all good distros. Relevant parties may not respond within a reasonable timeframe, or be interested, at which point going public becomes an option.

As we write this, the most recent vulnerability that might affect us is CVE-2019-9553, a buffer overflow in the venerable wget - a command line utility for fetching things (most probably webpages) via HTTP. Using the tool to download a maliciously crafted file could result in arbitrary code execution, and a very bad day.

![](img/7a0a282248f9658f0c87e55744c797b6_85_0.png)

![](img/7a0a282248f9658f0c87e55744c797b6_85_1.png)

![](img/7a0a282248f9658f0c87e55744c797b6_85_2.png)
