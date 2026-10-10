![](bbox=[0.19, 0.08, 0.8, 0.45])

Figure 21.5 *Gomoku*

# ## Zoning Out

Zone-mode isn't a game; it's just an amusing screen hack. You could call it a text-based screen saver. When this mode is active, it waits for a configurable number of seconds of inactivity (no mouse or keyboard action). A randomly-chosen text-distortion function is called that does strange things to your buffer until the next mouse or keyboard action occurs. Depending on which function is called, the text in your buffer might begin rotating, the case of letters might shift randomly, or letters might begin to drip and flow to the bottom of the screen. There are 15 different distortion functions. Needless to say, the distortion is only temporary; don't worry about your carefully-crafted prose!

Zone-mode works only with GNU Emacs, although it might be ported to XEmacs someday.

Start the mode by pressing M-x and typing

```
zone
```

Zone-mode doesn't lend itself to static screen shots, because the text-warping functions rely on motion for their effects. If you want it to quit, press M-x and type

```
zone-leave-me-alone
```