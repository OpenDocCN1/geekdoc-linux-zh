# # Do Not Forget
# What People Fetch

> The powerful iptables is intuitive enough even for lazy geeks to write their own rules.

![](bbox=[0.07, 0.29, 0.35, 0.51])

Nick Petreley, Editor in Chief

Let’s talk about protecting your network from what people can fetch. I’m going to take a twisty road to get there, so please stick with me.

I wrote a lengthy report published at www.theregister.co.uk/security/ security_report_windows_vs_linux that you might want to peruse. Allow me a couple caveats. The report is old, dated October 2004. Don’t e-mail me about the minor editing errors in the text that I never went back to fix. They don’t affect the thrust of the report.

Anyway, I hope you read the whole report, but I reference it primarily to draw out a single point. The Summer 2004 Evans Data Linux Developers Survey states that 78% of Linux developers have never had a Linux machine compromised. The Evans survey didn’t explore the nature of the very few Linux incidents that did occur. For example, some may have been victims of an Apache worm. Apache runs on both Linux and Windows, so those incidents would not be unique to Linux. More important, the same Apache worm that made the rounds many years ago could do much more damage on Windows than on Linux.

There’s a reason for that. It doesn’t take a rocket scientist to figure out that Windows is far more vulnerable to serious security breaches than Linux. Vista will not improve things. Microsoft seems more interested in preventing users from bypassing DRM restrictions than preventing crackers from breaking into Windows.

You can probably protect both Windows and Linux users from outside attacks simply by putting them behind a NAT-enabled router. A Linux-based router or even a cheap OTS box will usually do. The problem is that many security breaches occur not due to incoming attacks, but because people fetch tainted Web pages, download infected software or fetch myriad other file types with embedded code that exploits all the holes in Windows that allow people to escalate privileges and compromise the entire Windows box. If everyone ran Linux, this might not be such a big problem. Not everyone runs Linux. My kids use Linux, but they also use Windows. This is not only a family issue though. You may be in charge of a network where employees run Windows.

Here’s what I’ve done to protect my kids. First, I have taken great pains to limit their Web browsing to Firefox and their e-mail correspondence to Thunderbird. This avoids the common IE and Outlook exploits. Second, even though they access the Internet through a wireless NAT-enabled router, that router is connected to a Linux server that examines and filters what gets through before passing the traffic on to the Internet. I use Linuxbox with DansGuardian to block content. I use MIME filters to prevent potentially dangerous e-mail attachments from getting in. But, the coup de grâce is what I can do with iptables.

Before I continue, let me add a little perspective. I’d never consider myself competent enough to be a Linux kernel developer, but I have contributed a few lines of code to the kernel, and I have patched my own kernel to work around things like a stubborn ASUS motherboard that refused to shut down (the patch was too quick and dirty to be worthy of the kernel but it worked for me). I have also contributed code in various languages

to projects like Xoops, Lphoto and more. My point is that I’m not just an editor; I’m a programmer and an incurable geek.

I’m a lazy geek, however. I would much rather defer to a GUI program to generate firewall rules than write my own. But iptables has become so intuitive that even lazy geeks can write their own rules. All I had to grasp was how iptables processes traffic in terms of pre-routng, forwarding and postrouting. For example, the following rule is one of many that precludes various attempts to access the Web through DansGuardian. I have many such rules, and they’re more specific (they specify the source IP address of various computers), but I’ll list a simplified version of the obvious one:

```
```
iptables -t nat -A PREROUTING -i eth1 -p tcp 
--dport 80 -j REDIRECT --to-port 8080
```
```

Beyond the intuitive knowledge of syntax, that’s almost an English expression. It says to redirect the NAT traffic coming in through eth1 from port 80 to port 8080. If your kids or employees are clever enough to try to access the Web through an external proxy, simply redirect those ports to port 8080 too. You can use DansGuardian to block most other attempts to sneak around this protection.

Our article “Starting a Linux Firewall from Scratch”, on page T80 should help you get started with iptables. There are far more comprehensive iptables tutorials on the Web, one being iptables-tutorial.frozontuf.net/ iptables-tutorial.html. But most of them explore the complexities of iptables that only a security expert would need. If your needs are light, like mine, don’t be afraid to explore iptables and take a shot at writing your own rules. You’ll find iptables much more friendly than you’ve ever imagined, and they’re indispensable as part of your security framework.

**Nicholas Petreley is Editor in Chief of Linux Journal and a former programmer, teacher, analyst and consultant who has been working with and writing about Linux for more than ten years.**