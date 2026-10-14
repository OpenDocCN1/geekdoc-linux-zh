On the Configure Filter screen (Figure 1-18), select the printer that most closely matches yours, then choose the appropriate paper size and resolution.

![](bbox=[0.26, 0.19, 0.88, 0.5])

Figure 1-18: Specifying printer model and specs

Press OK twice to return to the Print System Manager window, then select lpd • Restart lpd to activate your printer. When finished, select PrintTool • Quit to exit.

# CONFIGURING A SOUND CARD

To configure a sound card, enter the sndconfig command from a shell prompt. When the Sound Configuration Utility screen appears (Figure 1-19), press OK to probe your system. If the probe finds a sound card it can autoconfigure, it will do so. Otherwise you must select your sound card from a list and enter the port, IRQ, and DMA information. The information you got from the Windows Device Manager will help you here. After making your selections, sndconfig will play sound and music clips and ask if you could hear them. If not, go back and try different settings.