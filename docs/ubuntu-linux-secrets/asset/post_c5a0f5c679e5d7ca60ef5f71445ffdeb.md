
outside intruders, while still allowing you to send email messages, browse the Internet, and connect to remote devices such as FTP and Windows servers.

You can customize how Firestarter operates by setting policies (rules) that either lock down or open up specific TCP and UDP ports on your workstation. After starting Firestarter program from either the Applications or System menu, you'll see the main Firestarter control window, shown in Figure 14-17.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_390_0.png)

Figure 14-17: The main Firestarter control window.

The main window shows the current status of the firewall (either active or disabled), the number of connection attempts (called events) that the firewall blocked, and the general network activity of the network interface Firestarter is protecting.

You control the Firestarter firewall using the three tabbed windows in the control window and the three buttons in the toolbar. The following sections describe these features in more detail.

## Tabbed Windows

The Firestarter control window uses three tabbed windows to control the operation of the firewall:

- Status: Provides a summary of the firewall operation.
- Events: Displays a detailed list of blocked connection attempts.
- Policy: Allows you to set additional rules to block or allow specific network traffic.

The Events tab displays a list of all the connection attempts Firestarter blocked on your workstation, as shown in Figure 14-18.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_391_0.png)

**Figure 14-18:** The Firestarter Events display.

The individual columns provide information about the event, such as the remote host that attempted to connect, the port number it attempted to connect to, and the name of the service that normally uses that port. You can add or remove columns to this display in the Preferences dialog box, as discussed in the next section.

The Policy tab allows you to define additional rules to the default rules. The Policy tab has a drop-down box that allows you to select which rules you're modifying:

- Inbound traffic policy
- Outbound traffic policy

When you select the outbound traffic policy, you'll notice that the default setting is to be permissive by default, allowing all outbound network connections. Right-click in the list box to add a rule to block specific network activity from the workstation, as shown in Figure 14-19.

The top list box allows you to block all network connectivity to all ports on a specific host, while the bottom list box allows you to block all network activity to all hosts on a specific port.

Alternatively, you can change the default behavior to be restrictive, blocking all outbound network connections by default. In this case, any hosts or ports you add to the list box are allowed instead of blocked.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_392_0.png)

Figure 14-19: Blocking specific outbound network traffic in Firestarter.

## The Toolbar

The Firestarter toolbar is pretty basic, but it provides crucial control over the firewall. The toolbar changes depending on which tabbed window you're viewing:

- Status: Displays the Preferences, Lock Firewall, and Start/Stop Firewall buttons.
- Events: Displays the Save List, Clear, and Reload buttons.
- Policy: Displays the Add Rule, Remove Rule, Edit Rule, and Apply Policy buttons.

In the Status window, Start/Stop Firewall buttons provide an easy way to activate and disable the firewall. The Lock button locks down the firewall so you (or anyone else on the system) can't accidentally change the current status.

The Preferences button in the Status window provides a dialog box for setting various configuration features on the firewall, shown in Figure 14-20. Firestarter divides the configuration settings into eight categories:

- Interface: Enable or disable the Firestarter panel icon applet.
- Events: Configure the behavior of the Events window by listing hosts and ports to not report events for and setting Firestarter to skip duplicate event entries in the log.
- Policy: Set policy rules to apply immediately after defining them.
