```
print MY_CMDFILE "plot \"$datafile\" with $lineform ";
print MY_CMDFILE "title \"$linetitle\"\n";

close(MY_CMDFILE);

# EOF
```

The code shown in bold is an example of how to deal with changes inside the datasets. Assume the value of 100 is sufficient regarding the y-axis; if there are more than 100 connections, then the script scales the y-axis to the highest value + 10 and stores this value in max. As long as there are no values > 99, max stays at 100. Figure 3.3 shows a graph with a scaled y-axis and Figure 3.4 with the default y-axis.

![](bbox=[0.22, 0.45, 0.82, 0.78])

# FIGURE 3.3 Graph with a scaled axis.

At the moment, the script automates only the creation of the command file. If you want to create the graphic at the same time, you have to make a choice between two approaches. Either you add two lines to the script, $gnuplot = "/usr/local/bin/gnuplot"; in the #Variables section and exec("$gnuplot $cmdfilepath/$cmdfilename"); or you create another script that takes care of the creation of the graphs. Listing 3.19 shows a script doing just that.

# LISTING 3.19 Script to Create the Graphs

```
#!/usr/bin/sh
```