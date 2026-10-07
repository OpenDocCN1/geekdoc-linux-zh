# **Calling a Remote Text-Mode System**

One of the simplest types of outgoing modem connection is a text-based link to another computer. The idea behind such a link is similar to that of using a serial port along with a dumb terminal or a computer running a terminal program. The difference is that a pair of modems and the telephone network sit between the two computers. In such a setup, the dial-out computer ordinarily functions as the terminal; the dial-in system runs a getty program and receives the call, as described shortly, in “Accepting Text-Mode Logins.”

Using modems in text mode is now much less common than it was before the rise of the Internet and PPP connections. It can still be a good way to handle simple access needs, however. Further, some companies still operate *bulletin-board* systems (BBSes), which provide product information, file downloads, and discussion forums for those without Internet access.

To call a remote text-based system, you must use a terminal program. Two popular terminal programs on Linux are the text-based minicom and the X-based Seyon (shown in Figure 11.4). Details of how to use these programs differ, but the basic principles are the same:

![](bbox=[0.11, 0.35, 0.85, 0.86])

+   - Before you run a program, you may need to create a symbolic link so that `/dev/modem` points to the device file on which your modem resides (such as `/dev/ttyS0`). Alternatively,