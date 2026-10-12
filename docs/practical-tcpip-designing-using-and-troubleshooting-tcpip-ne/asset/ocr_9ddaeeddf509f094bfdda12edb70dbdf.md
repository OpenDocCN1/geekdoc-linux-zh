times can give you a pointer to where the problem lies. We've occasionally seen messages sent to us that have sat for hours on some virus-scanning or content-filtering machine on the sender's site, only to be released late at night (see Module 25.2).

Timestamps are often not very accurate because computer clocks often drift over time. (The clock on one of our server machines had drifted about 12 minutes in 10 weeks uptime.) It's a good idea to run NTP (Network Time Protocol – Module 17.13) to keep all your clocks in sync.

Most e-mail clients show only selected mail headers, to save space on the screen and to avoid confusing users who just want to read the content of their mail messages and not the gory details of every machine the message happened to pass through. When you *do* want to see all the headers, you choose specifically to display them. Figure 11.5 shows Outlook's display of the headers (select message > File > Properties > Internet).

![](bbox=[0.25, 0.3, 0.78, 0.52])

**Figure 11.5** Outlook's header displays

Figure 11.6 shows Outlook Express (select message > File > Properties > Details).

![](bbox=[0.25, 0.6, 0.78, 0.83])

**Figure 11.6** Outlook Express: select message

In Netscape, you set an option for the level of header detail to be displayed in the message windows using the menu View > Headers > All.

In the next module we explain how the client receives messages using POP.