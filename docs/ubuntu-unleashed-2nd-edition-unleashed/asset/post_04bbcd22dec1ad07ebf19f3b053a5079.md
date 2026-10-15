
talented computer hackers or allow visitors to plug computers into your network, the worst internal attack you are likely to encounter is from a disgruntled employee.

## Hacker Versus Cracker

In earlier days, there was a distinction made between the words hacker and cracker. A hacker was someone who used technology to innovate in new or unusual ways, whereas a cracker was someone who used technology to attack another's computers and cause harm.

This distinction was lost on the general public, so the term hacker has now come to mean the same as cracker. This book follows general usage, so a hacker is a malicious person using his computer to cause problems for others.

Although you should never ignore the internal threat, you should arguably be more concerned with the outside world. The big bad Internet is a security vortex. Machines connected directly to the outside world can be attacked by people across the world, and invariably are, even only a few minutes after having been connected.

This situation is not a result of malicious users lying in wait for your IP address to do something interesting. Instead, canny virus writers have created worms that exploit a vulnerability, take control of a machine, and then spread it to other machines around them. As a result, most attacks today are the result of these autohacking tools; there are only a handful of true hackers around, and, to be frank, if one of these ever actually targets you seriously, it will take a mammoth effort to repel him regardless of which operating system you run.

Autohacking scripts also come in another flavor: prewritten code that exploits a vulnerability and gives its users special privileges on the hacked machine. These scripts are rarely used by their creators; instead, they are posted online and downloaded by wannabe hackers, who then use them to attack vulnerable machines.

So, the external category is itself made up of worms, serious day job hackers, and wannabe hackers (usually called script kiddies). Combined they will assault your Internet-facing servers, and it is your job to make sure your boxes stay up, happily ignoring the firefight around them.

On the internal front, things are somewhat more difficult. Users who sit inside your firewall are already past your primary source of defense and, worse, they might even have physical access to your machines.

Regardless of the source of the attack, there is a five-step checklist you can follow to secure your box:

- 1. Assess your vulnerability. Decide which machines can be attacked, which services they are running, and who has access to them.
- 2. Configure the server for maximum security. Only install what you need, only run what you must, and configure a local firewall.
- 3. Secure physical access to the server.
- 4. Create worst-case-scenario policies.
- 5. Keep up-to-date with security news.

Each of these is covered in the following sections, and each is as important as the others.

## Assessing Your Vulnerability

It is a common mistake for people to assume that switching on a firewall makes them safe. This is not the case and, in fact, has never been the case. Each system has distinct security needs, and taking the time to customize its security layout will give you maximum security and the best performance.

The following list summarizes the most common mistakes:

- Installing every package—Do you plan to use the machine as a DNS server? If not, why have BIND installed? Go through Synaptic and ensure that you have only the software you need.
- Enabling unused services—Do you want to administer the machine remotely? Do you want people to upload files? If not, turn off SSH and FTP because they just add needless attack vectors. This goes for many other services.
- Disabling the local firewall on the grounds that you already have a firewall at the perimeter—In security, depth is crucial: The more layers someone has to hack through, the higher the likelihood she will give up or get caught.
- Letting your machine give out more information than it needs to—Many machines are configured to give out software names and version numbers by default, which is just giving hackers a helping hand.
- Placing your server in an unlocked room—If so, you might as well just turn it off now and save the worry. The exception to this is if all the employees at your company are happy and trustworthy. But why take the risk?
- Plugging your machine into a wireless network—Unless you need wireless, avoid it, particularly if your machine is a server. Never plug a server into a wireless network because it is just too fraught with security problems.

After you have ruled out these, you are onto the real problem: Which attack vectors are open on your server? In Internet terms, this comes down to which services are Internet-facing and which ports they are running on.

Two tools are often used to determine your vulnerabilities: Nmap and Nessus. Nessus scans your machine, queries the services running, checks their version numbers against its list of vulnerabilities, and reports problems.
