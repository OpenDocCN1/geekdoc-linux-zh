system go up against Checkpoint or a PIX and come out on top---for tens of thousands of dollars less.

# # Configuring PF

Configure PF in /etc/pf.conf. This file contains statements and rules whose formats vary with the features they configure. Not only is the rule order extremely important but also the order in which features are configured. If you try to do stateful inspection before you reassemble fragmented packets, for example, connections won't work properly.

The default /etc/pf.conf has the sample rules in the proper order, but if you're in the slightest danger of becoming confused, I suggest that you put large comment markers between the sections, in capital letters if necessary. (Use hash marks to comment pf.conf.) The features must be entered in this exact order:

+   1. Macros
+   2. Tables
+   3. Options
+   4. Packet normalization
+   5. Bandwidth management
+   6. Translation
+   7. Redirection
+   8. Packet filtering

Yes, PF does more than just filter packets. It's a general-purpose TCP/IP manipulation tool. We won't cover all of its features here; go read Peter's book.

# ## Macros

A macro lets you define variables to make writing and reading rules easier. For example, here are macros to define your network interface and your IP address: