# ## Troubleshooting

Several things can go wrong when you use printers. This section discusses some of the most common problems and their solutions.

# ### Printer Does Not Receive Data; Jobs Are Sitting in Queue

Check lpq and make sure that the spooling daemon is running. If it says Warning: no daemon present, you will need to use lpc to restart the spooling daemon. Also check 1pc and make sure that the printer is not disabled.

# ### Data Light on Printer Flashes, but Printer Will Not Print

This is often a symptom of sending non-PostScript data to a PostScript printer. Check your filter and make sure it is filtering text correctly and converting that text to PostScript.

# ### Printing an Image File in GIMP or a Web Page Results in Hundreds of Pages of Garbage Being Printed

This can often be a symptom of feeding PostScript data to a printer that doesn't understand PostScript. The non-PostScript printer will try to print this file as plain text. Check out the GhostScript program and also see the section earlier in this chapter titled “Printing PostScript Files on Non-PostScript Printers.”

# ### The Printer Is Slow

Try setting the printer to polled mode (assuming this printer is on the parallel port). Use the following command:

```
lptcontrol -p
```

Remember that you will need to add this to a startup file if you want it to take effect at each system boot. See the section at the beginning of the chapter on lptcontrol.

# ### Printed Output “Stair Steps”

The symptoms of the stair-step problem look something like this:

```
Line one of the file.
    Line two of the file.
        Line three of the file.
            Line four of the file.
```

This pattern will continue until the text runs off the end of the page. This is a fairly common problem caused by differences in the way Unix and DOS/Windows interpret the linefeed (LF) character. When DOS/Windows advances to a new line, it sends both a carriage return and a linefeed. Unix, on the other hand, sends only a linefeed character