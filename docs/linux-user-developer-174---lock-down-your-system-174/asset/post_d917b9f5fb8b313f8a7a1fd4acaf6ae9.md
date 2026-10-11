
![](img/1f330653f83dcf0397f7d224ce8bbc16_34_0.png)

Above gnuplot can be used to plot commonly used mathematical functions

```
gnuplot

  G N U P L O T
 ...
  Terminal type set to 'wx'
  gnuplot> plot sin(x)
```

Entering the command sequence printed leads to a pop-up display showing the contents of Figure 1.

While this is not an unattractive option, the product is capable of a lot more. This is accomplished by setting state variables; the gnuplot program, even in interactive mode, is not completely stateless. One way to try this out involves the following command sequence, which is ideally entered right after you've started gnuplot:

```
gnuplot> set grid
  gnuplot> plot sin(x), cos(x)
  gnuplot>
```

When done, you are presented with the output shown in Figure 2. It is obvious that the set grid command motivates the program to display a grid in the background of any rendered diagrams. Be aware that Ctrl+Q does not exit the gnuplot application – getting back to the operating system can only be accomplished by entering the quit command followed by the Return key.

You've welcome HERE

Even though running gnuplot directly is a fun way to get some charts on the screen, shell scripts work better if they can control the execution en masse via a set of parameters defined during

> Humans are less suited to processing text and perform much better when provided with graphical input

![](img/1f330653f83dcf0397f7d224ce8bbc16_34_1.png)

Above Setting the grid property enhances diagram output by including a backdrop grid

The creation of the script file. Embedding long sequences of text into shell scripts is best handled via the concept of a here document: it is a set of syntax markups that allow you to embed a long string into a shell script. Start out with the following example that demonstrates its use:

```
#!/bin/bash

gnuplot <<EOFTHISDOC
  set terminal wx
  plot sin(x), cos(x)
  EOFTHISDOC
```

In Bash, shell scripts containing HERE documents start out via a specified start-up sequence. This set of characters – in the case of our example, we use END OF THIS DOC – must have something that does not occur in the actual textual content found inside your document. Instead, it should act as a delimiter on the other side. In the case of our example, the here document consists of the set terminal and plot commands, which get passed into the main gnuplot invocation via the <& command.

Running the current version of the program leads to unsatisfactory results. The window containing the chart will pop up shortly, only to disappear again afterwards. This stupid behaviour is caused by a little oddity of gnuplot – by default, it removes all chart windows from the screen the moment the main application reaches the end of the script input provided.

Fortunately, passing in the –persist parameter allows you to change this behaviour. A working version of our little charting program would look like this:

```
#!/bin/bash

gnuplot –persist <<EOFTHISDOC &
  set terminal wx
  plot sin(x), cos(x)
  EOFTHISDOC
```

Run this version of the program to find yourself in front of a diagram showing both sine and cosine – an excellent tool for teaching more about trigonometry.

## Off Licence!

Gnuplot's name, in fact, is misleading: the product is not distributed under the GPL licence, but uses a different licensing regime which does not permit the redistribution of changed source code packages. Developers must instead publish patches that can be applied against an officially released version of the program code.

## Tutorial | Bash masterclass

![](img/1f330653f83dcf0397f7d224ce8bbc16_35_0.png)

> **Linearise me**
> In some cases, transforming a set of values into a function is helpful as it allows the creation of more sophisticated models using the additional data generated from the function. This is a highly mathematical topic, which usually requires dedicated study of its own - O'Reilly's book *Mastering Algorithms in C* [http://ahop.oreilly.com/product/07811565924536.do] contains a pretty good, understandable discussion of the process of polynomial interpolation.

## File-a-Gogo!

In most cases, the data that needs to be displayed does not take the form of a simple function; it, instead, tends to come as a series of values which must be passed to gnuplot via the corresponding command line functions.

Embedding such information into the script is not particularly satisfactory - creating self-modifying shell scripts is an art of its own, which we cannot discuss in the frame of a single story. Fortunately, gnuplot can also take in plotting data from _.pub_ files. Let us demonstrate this by creating a file called datasource.txt, and by populating it with a bit of data taken from the precious metal powerhouse KitCo (data taken from [http://www.kitco.com/gold.londonfx.html].

| 1 | 1236.45 | 18.59 |
|---|---|---|
| 2 | 1267.5 | 18.75 |
| 3 | 1281.4 | 18.81 |
| 4 | 1282.35 | 18.86 |
| 5 | 1283.05 | 18.22 |
| 6 | 1302.8 | 18.3 |
| 7 | 1301 | 18.87 |
| 8 | 1303.75 | 18.54 |
| 9 | 1288.45 | 18.24 |
| 10 | 1272 | 17.76 |

A cursory look at the structure of the file reveals that we have three columns: in addition to a handling sequence number, we have both the silver and the gold prices for ten consecutive trading days. Displaying this information in a naive chart can be accomplished with the following bit of code:

```
#!/bin/bash

gnuplot -persist <<ENDOFTHISDOC &
  set terminal wx
  plot 'datasource.txt' using 1:2, 'datasource.txt'
    using 1:3 with lines
  ENDOFTHISDOC
```

Here, two things are interesting. First of all, the file name is passed in using the _-monitor to designate the file name in question. Secondly, we specify which column numbers are used as the two variables. As we plan to create one diagram line with gold and one with silver information, two using commands are used that are tied together using the comma operator.

When done, run the program - its output will be similar to the one shown in the figure.

This is a common problem in diagrams: if the values to be displayed are of significantly differing ranges, the use of a common axis leads to problems. In the case of our diagram, gold price information looks good while the smaller silver price data gets squashed.

Fortunately, fixing the problem is really easy; change the here document in order to force gnuplot to use two independent axes:

```
#!/bin/bash

gnuplot -persist <<ENDOFTHISDOC &
  set terminal wx
  plot 'datasource.txt' using 1:2, 'datasource.txt'
  using 1:3 with lines
ENOFTHISDOC
```

**Above** One axis cannot be used to display two datasets efficiently if their values differ significantly

Our example will yield a diagram showing the two price curves in a somewhat sensible format; sadly, axis information is displayed only for the gold price. A long-term mentor of this author - duly equipped with a PhD in physics from one of the most reputable institutes of Austria - once failed the author of this story for a technicality; his diagrams lacked axis descriptions, and thus were 'meaningless'. While this might seem a bit extreme, adding context to diagrams is helpful as it prevents misinterpretation.

As one can imagine, this is easily accomplished in gnuplot via the following modifications:

```
#!/bin/bash

gnuplot -persist <<ENDOFTHISDOC &
  set terminal wx
  set y2label 'Gold'
  set y2label 'Silver'
  set xlabel 'Trading days'
  set y2tics autoref
  plot 'datasource.txt' using 1:2 axes x2y2 with lines
  'datasource.txt' using 1:3 axes x2y2 with lines
  ENDOFTHISDOC
```

We start out by using the _x-_ and _ylabel_ commands to assign textual descriptions to the axes. Next, the _y2tics_ attribute is set to _autofreq_: this instructs gnuplot to find the optimal step values using its internal logic. In addition to that, it also overwrites the default settings: if left to its own devices, gnuplot will display ticks only on the first axis of the diagram.

With that, it is time to run our standalone example for one last time. This figure shows what you can expect.

## File away!

Displaying diagrams is interesting as long as the shell script is run interactively - if your script is offline, it would be more interesting to create a file which can then be distributed via email or SCP transfer.

This can be accomplished by redirecting gnuplot's terminal instance to make it output information into the file rather than to a window shown on the frame buffer. Let's this by modifying the previous metal charting program - a happily abridged version omitting the state variable code for brevity looks like this:
