![](bbox=[0.52, 0.03, 0.92, 0.42])

# Hour 10

# Quoting

In the preceding chapter, you looked at substitution, which occurs automatically whenever you enter a command containing a meta-character or a $. The way the shell interprets these and other special characters is generally useful, but sometimes it is necessary to turn off shell substitution and let each character stand for itself. Turning off the special meaning of a character is called quoting, and it can be done in three ways:

+   - Using the backslash (\ )
+   - Using the single quote (')
+   - Using the double quote (")

Quoting can be a very complex issue, even for experienced UNIX programmers. In this chapter, you look at each of these forms of quoting and learn how to use them. You learn a series of simple rules to help you understand when quoting is needed and how to do it correctly.