
## Built-in Protection in the Kernel

A number of networking and low-level protective services are built in to the Linux kernel. These services can be enabled, disabled, or displayed using the `sysctl` command, or by echoing a value (usually a 1 or a 0 to turn a service on or off) to a kernel process file under the `/proc` directory. One of the newest features is the ExecShield kernel enhancement. This feature protects your system by randomizing the location of processes in virtual memory and disallowing execution of parts of memory after a program loads. See the Fedora Release Notes for more information.

## Understanding Computer Attacks

There are many ways in which computer attacks can be divided, but perhaps the easiest is *internal*, which are computer attacks done by someone with access to a computer on the local network, and *external*, which are attacks by someone with access to a computer through the Internet. This might sound like a trivial separation to make, but it is actually important: Unless you routinely hire talented computer hackers or allow visitors to plug computers into your network, the worst internal attack you are likely encounter is from a disgruntled employee.

## Hacker Versus Cracker

In earlier days, there was a distinction made between the words *hacker* and *cracker*. A hacker was someone who used technology to innovate in new or unusual ways, whereas a cracker was someone who used technology to attack another's computers and cause harm.

This distinction was lost on the general public, so the term *hacker* has now come to mean the same as *cracker*. This book follows general usage, so a *hacker* is a malicious person using his computer to cause problems for others.

Although you should never ignore the internal threat, you should arguably be more concerned with the outside world. The big bad Internet is a security vortex. Machines connected directly to the outside world can be attacked by people across the world, and invariably are, even only a few minutes after having been connected.

This situation is not a result of malicious users lying in wait for your IP address to do something interesting. Instead, canny virus writers have created worms that exploit a vulnerability, take control of a machine, and then spread it to other machines around them. As a result, most attacks today are the result of these autohacking tools; there are only a handful of true hackers around, and, to be frank, if one of these ever actually targets you seriously, it will take a mammoth effort to repel him regardless of which operating system you run.

Autohacking scripts also come in another flavor: prewritten code that exploits a vulnerability and gives its users special privileges on the hacked machine. These scripts are rarely used by their creators; instead, they are posted online and downloaded by wannabe hackers, who then use them to attack vulnerable machines.

So, the external category is itself made up of worms, serious day job hackers, and wannabe hackers (usually called *script kiddies*). Combined they will assault your Internet-facing servers, and it is your job to make sure your boxes stay up, happily ignoring the firehose around them.

On the internal front, things are somewhat more difficult. Users who sit inside your fire-wall are already past your primary source of defense and, worse, they might even have physical access to your machines.

Regardless of the source of the attack, there is a five-step checklist you can follow to secure your Fedora box:

1. Assess your vulnerability. Decide which machines can be attacked, which services they are running, and who has access to them.
2. Configure the server for maximum security. Only install what you need, only run what you must, and configure a local firewall.
3. Secure physical access to the server.
4. Create worst-case-scenario policies.
5. Keep up-to-date with security news.

Each of these is covered in the following sections, and each is as important as the others.

### Assessing Your Vulnerability

It is a common mistake for people to assume that switching on a firewall makes them safe. This is not the case and, in fact, has never been the case. Each system has distinct security needs, and taking the time to customize its security layout will give you maximum security and the best performance.

The following list summarizes the most common mistakes:

- **Installing every package**—Do you plan to use the machine as a DNS server? If not, why have BIND installed? Go through the Add/Remove Applications dialog and ensure that you have only the software you need.
- **Enabling unused services**—Do you want to administer the machine remotely? Do you want people to upload files? If not, turn off SSH and FTP because they just add needless attack vectors. This goes for many other services.
- **Disabling the local firewall on the grounds that you already have a firewall at the perimeter**—In security, depth is crucial: The more layers someone has to hack through, the higher the likelihood she will give up or get caught.
- **Letting your machine give out more information than it needs to**—Many machines are configured to give out software names and version numbers by default, which is just giving hackers a helping hand.
- **Placing your server in an unlocked room**—If so, you might as well just turn it off now and save the worry. The exception to this is if all the employees at your company are happy and trustworthy. But why take the risk?
- **Plugging your machine into a wireless network**—Unless you need wireless, avoid it, particularly if your machine is a server. Never plug a server into a wireless network because it is just too fraught with security problems.

After you have ruled out these, you are onto the real problem: Which attack vectors are open on your server? In Internet terms, this comes down to which services are Internet-facing and which ports they are running on.

Two tools are often used to determine your vulnerabilities: Nmap and Nessus. Nessus scans your machine, queries the services running, checks their version numbers against its list of vulnerabilities, and reports problems.

Although Nessus sounds clever, it does not work well in many modern distributions (Fedora included) because of the way patches are made available to software. For example, if you're running Apache 2.0.52 and a bug is found that's fixed in 2.0.53, Fedora backports that patch to 2.0.52. This is done because the new release probably also includes new features that might break your code, so the Red Hat team takes only what is necessary and copies it into your version. As a result, Nessus will see the version 2.0.52 and think it is vulnerable to a bug that has in fact been backported.

The better solution is to use Nmap, which scans your machine and reports on any open TCP/IP ports it finds. Any service you have installed that responds to Nmap's query is pointed out, which enables you to ensure that you have locked everything down as much as possible.

To install Nmap, select System Settings, Add/Remove Applications. Near the bottom of the list of applications is System Tools, where you can select Nmap-frontend and Nmap. Although you can use Nmap from a command line, it is easier to use with the front end—at least until you become proficient. To run the front end, select Actions, Run Application and run nmapfe. If you want to enable all Nmap's options, you need to switch to root and run nmapfe from the console.

The best way to run Nmap is to use the SYN Stealth scan, with OS Detection and Version Probe turned on. You need to be root to enable the first two options (they are on by default when you are root), but it is well worth it. When you run Nmap (click the Scan button), it tests every port on your machine and checks whether it responds. If it does respond, Nmap queries it for version information and then prints its results onscreen.

The output lists the port numbers, service name (what usually occupies that port), and version number for every open port on your system. Hopefully, the information Nmap shows you will not be a surprise. If there is something open that you do not recognize, a hacker might have placed a backdoor on your system to allow herself easy access.

You should use the output from Nmap to help you find and eliminate unwanted services. The fewer services that are open to the outside world, the more secure you are.
