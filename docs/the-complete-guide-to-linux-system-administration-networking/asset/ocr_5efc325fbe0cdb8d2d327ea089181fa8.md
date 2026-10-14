execute at any time from the command line. (A text-mode program to perform the same task is system-config-securitylevel-tui; you can also start this program using its old name, lokkit.)

Figure 15-14 shows a screen from the graphical system-config-securitylevel program. This program doesn't ask you about "rules," but instead sets up reasonable rules based on how secure you want your system to be and any specific protocols that you want to leave more open. (Remember that "more secure" means "harder to use" if you are in a trusted environment such as a testing lab, where you want to run many network services without reconfiguring the firewall for each one.)

![](bbox=[0.22, 0.36, 0.62, 0.74])

Figure 15-14 The system-config-securitylevel program

Because this program only sets a generalized "security level," a system administrator is well advised to download (or purchase, as warranted) a more complete graphical solution if the iptables command alone seems inefficient. Several examples are listed here:

+   - The GNOME program Firestarter includes a firewall creation wizard to help you set up a basic firewall. Then you can modify the basic iptables rules as needed within the graphical interface. You can also watch real-time monitors to see when a packet matches a specific rule. You can find this program through the download link on firestarter.sourceforge.net.

+   - Mason is a firewall tool that uses a different approach appropriate for less experienced Linux administrators. Instead of defining rules at the outset, you start Mason, then start all the other services that you want to support on your server. Mason prepares a list of rules that intelligently allows only those services and blocks all others. For more information, visit http://mason.stearns.org.