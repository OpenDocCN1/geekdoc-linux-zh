
case; however, treating all such incidents in this manner is an invitation to disaster. All it takes is for the attacker to have installed a "backdoor" of some kind that lets him return and cause much more destructive damage than before.

If you suspect you have been hacked, or "owned," here are some steps you must take:

- 1. Disconnect the system from the Net immediately. No matter what backdoors the attacker has installed in your system, he can't do anything if the system isn't on the network (in other words, it's behind an air gap). This prevents a hacker who realizes that he has been discovered from covering his tracks by wiping your hard disk clean.
- 2. Check `/var/cron/tabs` and `/etc/crontab` for new entries; also check `atq` for jobs the attacker has left to be run in his absence. The system may be off the network, but `cron` jobs will still run, and the hacker can still trash your system in this way unless you clear out any suspicious pending jobs.
- 3. Don't try to contact the attacker or let him know that you're on to him. Even after you've removed your system from harm's way, the attacker will vanish if he realizes you're trying to track him down, and law enforcement will have a much harder job finding him. Let him think you've simply taken the machine offline to recover from the damage.
- 4. Gather together your log files from `/var/log`, and wherever else your programs might have them, and comb them for entries that might indicate where the attacker came from and how he gained access. If you are running any services for which security bulletins have been recently posted, and you haven't updated those services to remedy their vulnerabilities, it's almost a certainty that that's how the attacker gained access.
- 5. Take as much useful information as you can find to the National Infrastructure Protection Center (NIPC) Web site, <http://www.nipc.gov> (or the equivalent for your country's cybercrime investigation agency, if you're not in the United States), and fill out an incident report. This arm of the FBI is in charge of investigating cybercrime and hacker activity, and provided they have enough concrete information from your affected data, they can swiftly track down the perpetrator. Most hacker activity is committed by *script kiddies*—casual vandals who use tools prepackaged by others to exploit certain known vulnerabilities. These types of hackers usually can be found and prosecuted quite successfully.
- 6. Back up your important data—Web documents, configuration files, home directories, and everything in `/usr/local`—and reinstall the operating system. To be really thorough, wipe the hard disk clean, reinstall FreeBSD from scratch, and restore the local data. Use the daily output of Tripwire to tell you to what extent you need to "nuke and pave" the machine; beware of backdoors that may have been installed among your own installed programs in `/usr/local`, or even among your Web documents or configuration files.
- 7. Update all your services to the most recent versions, referring to all relevant security bulletins, before putting the system back online. Be especially vigilant for the first few days after bringing the system back up; the hacker may continue to try to break in. Pay especially close attention to your log files during this period; the more evidence you can gather, the easier it will be for the NIPC and FBI to do their job.

## Denial of Service (DOS) Attacks

Although it isn’t technically a security issue, another type of malicious network activity has nonetheless become quite important to system administrators recently. This is the Denial of Service (DOS) attack.

DOS attacks don’t involve any compromise of a system’s security or privacy. Rather, they are simply brute-force floods, sending so much traffic over a network that legitimate traffic is lost in the shuffle. The goal is often to crash the server through sheer overwhelming volume of data and number of requests. These kinds of attacks are much harder to defend against than directed hack attacks, which can be foiled through the use of IPFW, PortSentry, and the other tools we have already discussed. The impact of a DOS attack cannot be eliminated; it can only be mitigated because DOS attacks are made up completely of legitimate traffic, indistinguishable from your actual mission-critical data flow. The problem is just that there’s too much of it.

Sometimes, a DOS attack can be identified as coming from a certain source, and you can block it by adding a firewall rule to deny traffic from or to that source. However, many recent attacks hide the actual source—ping (ICMP) broadcast attacks look as if they’re coming from a certain source address, which is actually the victim address that receives the brunt of the attack. Distributed DOS, or DDOS, attacks work even more insidiously, with hundreds or even thousands of compromised desktop machines unwittingly taking part in the attack, or tracking down the actual culprit is pretty much impossible.

Certain configuration options in various servers and in the kernel can help to prevent your system from completely submerging during a DOS attack. The following sections look at a few of these measures; however, bear in mind that they can only serve to increase your system’s chances of surviving a DOS attack—they can’t neutralize the attack itself, nor can they guarantee that the attacker won’t simply try harder until your system does succumb.

### Limiting Server Forks

Many DOS attacks are targeted against services such as Apache, Sendmail, or others that operate by *forking* a new process to handle each incoming request. If an attacker sends an overwhelming number of requests to the service, it will fork off so many processes that the CPU and memory will eventually become exhausted, possibly destabilizing your system.

You can mitigate the risk of a server fork attack by making sure that all your forking services have built-in limits to the number of simultaneous child processes they can have. These limitations can impact the services' ability to fulfill legitimate requests during normal operation, but that tradeoff may be worth saving you during a DOS attack.

Apache has a MaxClients directive (by default set to 150) that keeps more than that number of requests from being serviced at once. A wily attacker, however, can repeatedly request a processor-intensive CGI script until Apache is creating executable processes faster than they can complete. Requests for executable processes are much more likely to trigger a runaway server than are requests for static HTML pages. If you can get the system to accept a Telnet or SSH login, shut down Apache (`apachectl stop`) until the attack is over. That may be the only way to recover from such an attack.

Fortunately, most HTTP DOS attacks are traceable to a single client IP address, which you can block with IPFW rules or with a `deny from` directive in Apache itself. If this doesn't work, though, you can always decrease MaxClients to the point where even if the server is maxed out, the clients can't swamp it.

There's a similar feature in Sendmail: `MaxDaemonChildren`, disabled by default, which you can enable by uncommenting it in `/etc/mail/sendmail.cf` directly and restarting the server (`make restart`). Apart from this, Sendmail has a built-in brake that prevents it from starting new processes if the system load is over 12; however, this mechanism has too much lag during a fast-moving attack for the server to respond well, so it may be necessary to explicitly limit the number of children Sendmail can have at a time.

> **TIP**  
> Other directives in Sendmail that you can use to help foil attackers (or anybody using your server too aggressively) are `QueueLA`, `RefuseLA`, `DelayLA`, and `ConnectionRateThrottle`. These directives are documented with comment lines in `sendmail.cf` itself and should be fairly self-explanatory. For instance, `QueueLA` (which in its default state is set to 8, but disabled) can be uncommented to make Sendmail queue messages automatically rather than attempting to deliver them, if the load average is higher than 8.

A potential general solution to fork attacks, even defending against those that might originate from your own system (a renegade or clumsy user, for example), is to modify `/etc/login.conf` to put limits on the CPU, RAM, and open file usage that a user can have. Create a class for the user that runs the service in question—nobody in the case of Apache, or an individual local user whose resources you want to limit—and use `efhn` to put the user into the class. An example `login.conf` class might look like this:

```
badesvr:\
	:cputime=30m:\
	:openfiles=24:\
	:maxproc=32:\
```

![](img/48eec858cce7dfb89da36a4d40b7daf3_754_0.png)
