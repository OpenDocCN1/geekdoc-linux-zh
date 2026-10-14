This is very similar to the command file in the previous example, except for the following differences: The title is changed; the command to turn off the key is not printed; the name of the output file differs; and in the long last plot line, columns two through three are each plotted against the first column (the month names) in the input file, each with the linespoints style as before, but each with its own label for the key.

⇒ To process the commands in temperature2.gnuplot, type:

```
$ gnuplot temperature.gnuplot [RET]
```

This command starts gnuplot and runs the commands in the file temperature2.gnuplot. A new PostScript file, temps2.ps, is written, which looks like Figure 29-7. (While the printed illustration is in black and white, the actual image created from this command has colored plots.)

![](bbox=[0.2, 0.55, 0.85, 0.8])

Figure 29-7. The temps2.ps file.

# 29.9 Using Other Mathematics Tools

The following table lists some of the other more popular mathematics-related tools available for Linux.