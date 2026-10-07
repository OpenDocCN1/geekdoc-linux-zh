# Chapter 2: Command Syntax 93

The >out part says that stdout will go to file out. The 2>&1 part says that fd 2 (stderr) will go to the same place as fd 1 (stdout).

![](bbox=[0.035, 0.163, 0.128, 0.243])

Watch the spacing on this. There must be no spaces between the fd number, the (>), and the ampersand.

+   a) Why must there be no space between the 2 and the (>)?

# LAB 2.3

+   b) Why must there be no space between the (>) and the ampersand?

Spaces after the ampersand are optional.

+   c) Why can there be a space between the ampersand and the 1?

Remember that I/O redirection symbols are processed by the shell in left-to-right order.

+   d) What is the difference between the following two commands:
cat out1 out2 >out3 2>& 1
cat out1 out2 2>& 1> out3