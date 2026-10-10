
## Removing Print Jobs from the Queue

The `lprm` or `cancel` command removes one or more jobs from the print queue. There are several ways to issue this command:

- If it's issued with a number, that number is understood to be the job ID (as shown in `lpq`'s output) that's to be deleted.
- If root runs the BSD `lprm` and passes a dash (`-`) to the program, it removes all print jobs belonging to all users.

The `lprm` and `cancel` programs may be run by root or by an ordinary user, but as just noted, their capabilities vary depending on who runs them. Ordinary users may normally remove only their own jobs from the queue, but root may remove anybody's print jobs. (CUPS does provide an option, which can be set from the Web interface, to enable ordinary users to cancel other users' jobs, but this option is not set by default.)

Instead of using `lprm` or `cancel`, you may use the Web interface for CUPS to remove jobs from a print queue. Click the **Jobs** tab (shown in Figure 9.3) to obtain a list of current print jobs. Click **Cancel Job** in the row for any particular job to cancel it.

## Controlling the Print Queue

In the original BSD LPD system, the `lpc` utility starts, stops, and reorders jobs within print queues. Although CUPS provides an `lpc` command, it has few features. Instead of using `lpc`, you should use the CUPS Web interface, which provides point-and-click print queue management:

- You can disable a queue by clicking the **Stop Printer** link for the printer on the CUPS Web interface (see Figure 9.3). When you do so, this link changes to read **Start Printer**, which reverses the effect when clicked. The **Jobs** tab also provides a way to cancel and otherwise manage specific jobs.
- You can use a series of commands, such as `cupsenable`, `cupsdisable`, and `lpmove`, to control the queue. These commands enable a queue, disable a queue, or move a job from one queue to another. Moving a job can be handy if you must shut down a queue for maintenance and want to redirect the queue's existing jobs to another printer.

## Summary

Beyond basic network configuration lie increasingly advanced network configuration tasks. Router and firewall configurations are two such sets of tasks. You can enable a computer with two or more network interfaces to pass data between network segments, thus linking them, either on a multisegment private network or to link one network to the Internet. Firewall configurations can improve the security of router configurations, but firewalls are also important security tools for nonrouter computers. In Linux, you use the `iptables` program to create firewalls.

Two types of server programs that you're likely to run on Linux are remote login tools and printing tools. Basic remote login tools permit text-mode access to the computer. Although Telnet was historically popular for this task, today SSH has largely supplanted Telnet because of SSH's superior security features. In addition to supporting encryption, SSH supports file transfers and tunneling a wide variety of protocols, which enables the addition of encryption features to otherwise unencrypted protocols. This feature is frequently used in conjunction with X, so users can log into a Linux system remotely and run X-based programs without taking special steps. You can also use X remotely without tunneling it through SSH, but this requires extra steps to link the client and servers. In some environments, you may want to reconfigure your X and XDMCP servers to permit remote GUI logins.

Printing in Linux is a network task; even on an isolated workstation, the CUPS print queue is a network-enabled tool, and it uses network protocols locally to do its work, much like X on an isolated system. CUPS really shines in a networked environment, though; it supports automatic printer discovery so that all the printers on a network may be shared by all the computers, with no need to explicitly configure these printers except on the computer that most directly manages them. Command-line tools such as `lpr`, `lprm`, `lpq`, and `lpstat` enable you to submit and manage print jobs; or you can use CUPS's Web-based tools to manage the task.

## Exam Essentials

Explain the function of a packet-filter firewall. A packet-filter firewall filters network traffic based on low-level data that's easily obtained from individual network packets without reassembling them into a complete data stream. Examples include source and destination IP addresses and port numbers. Such filters can protect a computer or (when used on a router) a network from certain types of suspicious network traffic, such as off-site attempts to access sensitive servers intended for local use.

Summarize how a packet-filter firewall is created in Linux. The usual tool for creating a packet-filter firewall is `iptables`. Each call to this utility creates an individual rule, such as one to drop incoming packets to a particular port from certain IP addresses. Many such rules combine together to create a complete firewall. Typically, a script runs at system startup to manage this task.

**Describe common text-mode remote login tools.** Telnet was the traditional remote text-mode login tool, but it passes data over the network unencrypted and so is a poor choice today. The Secure Shell (SSH) is the most common remote text-mode access tool today.

**Explain the nature of X clients and servers.** An X server controls a screen display and handles input from the user’s mouse and keyboard. Therefore, the X server is used directly by the user, and X clients are the programs that rely on the X server’s services.

**Explain the role of an XDMCP server.** An XDMCP server, such as XDM, KDM, or GDM, launches X and controls access to X via a login prompt—that is, it serves as Linux’s GUI login system. XDMCP servers are also network enabled, providing a way to log in remotely from another X server.

**Explain the role of Ghostscript in Linux printing.** PostScript is the standard Linux printing language, and Ghostscript converts PostScript into bitmap formats that are acceptable to non-PostScript printers. Thus, Ghostscript is a critical translation step in most Linux print queues.

**Summarize how print jobs are submitted and managed under Linux.** You use `lpr` or `lp` to submit a print job for printing, or an application program may call `lpr` or `lp` itself or implement its functionality directly. The `lpq` or `lpstat` utility summarizes jobs in a queue, and `lprm` can remove print jobs from a queue.

## Review Questions

1. What is the default port used by the Simple Mail Transfer Protocol (SMTP)?
   - A. 143
   - B. 80
   - C. 25
   - D. 21

2. Which of the following ports are known as unprivileged ports?
   - A. Those that have numbers above 1024
   - B. Those that have numbers between 512 and 1024
   - C. Those that have numbers between 1 and 100
   - D. Those that have numbers below 1024

3. Which port, by default, is commonly used by OpenSSH?
   - A. 20
   - B. 21
   - C. 22
   - D. 23

4. Which port, by default, is commonly used by HTTPS?
   - A. 111
   - B. 143
   - C. 389
   - D. 443

5. Which of the following is true of the DROP policy for iptables?
   - A. It replies as if the computer was available but running no software on the target port.
   - B. It ignores packets, providing the illusion of a network error between the sender and recipient.
   - C. It may be used only on ports that are opened by servers, not clients.
   - D. It may be applied as a default policy but not on a port-by-port basis.
