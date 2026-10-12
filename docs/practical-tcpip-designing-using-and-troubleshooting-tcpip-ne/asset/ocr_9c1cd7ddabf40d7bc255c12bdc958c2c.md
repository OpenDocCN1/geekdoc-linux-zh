# 13.3 Lab – a typical ethereal session

+   run **ethereal** without any command-line options: the **ethereal** window appears, with three empty panes (Figure 13.2)

![](bbox=[0.24, 0.16, 0.78, 0.37])

**Figure 13.2 The ethereal window**

+   select menu **Capture > Start** (or press Ctrl-k) to get the **Capture Preferences** window with its default options (Figure 13.3(a) shows Linux, Figure 13.3(b) shows NT):

+   a. we always change the options to **Update list of packets in real time**, and not to **Enable name resolution**. (We could have done this by using options -S and -n on the command line.)

+   b. enter the **Filter** you want, if any. This is the capture filter – which you can also enter with the **-f option** on the command line

![](bbox=[0.12, 0.62, 0.43, 0.84])

![](bbox=[0.44, 0.62, 0.71, 0.84])

![](bbox=[0.72, 0.62, 0.88, 0.84])

**Figure 13.3 Capture Preferences dialogs:**
(a) Linux
(b) Windows

**Figure 13.4 Capture window**