# FIGURE 13.3

diald Control window.

![](bbox=[0.28, 0.11, 0.73, 0.43])

The Interface lines show all lines and their states. The next section shows detailed link status. There are a couple of pretty graphs showing link activity.

From `dctrl`, you can force a link up or down or even force `diald` to exit completely. For this reason, the FIFO should be accessible only by root or someone you trust; see `dctrl(1)` for more details.

# ## kppp

The `kppp` program is a graphical KDE program for dialing out using a PPP link. It has excellent online help and is simply a front-end for `pppd`. Having read this chapter, you should have no problems understanding `kppp` and using it to set up a PPP link.

All the PPP settings are accessible from the Setup button. On the Modem tab, you can press the Terminal button and type directly to your modem. This is handy for debugging chat scripts.

# # Summary

In this chapter, you have learned how serial hardware is named and configured on Linux. You learned how to run `pppd` to bring up a PPP link and how to use `chat` to dial and log in to a remote computer. Next, you learned how PPP uses PAP and CHAP authentication for security, and how to link a personal workstation to an ISP. You then learned more advanced PPP scenarios, such as how to set up a remote access server and how to modify the routing table as a PPP link comes up and go down. Finally, you learned how to create on-demand PPP links with `diald` and how to use the graphical `kppp` application to set up a PPP link.