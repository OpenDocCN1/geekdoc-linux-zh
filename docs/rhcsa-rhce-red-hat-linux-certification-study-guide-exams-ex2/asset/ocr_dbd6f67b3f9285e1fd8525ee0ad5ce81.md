You should know how to use the two basic modes of vi: command and insert. When you use vi to open a file, it opens in command mode. Some of the commands start insert mode. Opening a file is easy; just use the vi filename command. By default, this starts vi in command mode. An example of vi with the /etc/nsswitch.conf file is shown in Figure 3-4.

The following is only the briefest of introductions to the vi editor. For more information, there are a number of books available, as well as an extensive manual formatted as a HOWTO available from the Linux Documentation Project at www.tldp.org. Alternatively, a tutorial is available through the vimtutor command.

# vi Command Mode

In command mode, you can do everything to a text file except edit it. The options in command mode are broad and varied, and they are the subject of a number of book-length texts. In summary, options in vi command mode fall into seven categories:

+   - **Open** To open a file in the vi editor from the command line interface, run the vi filename command.
+   - **Search** For a forward search, start with a backslash (/), followed by the search term. Remember, Linux is case sensitive, so if you're searching for

![](bbox=[0.07, 0.68, 0.88, 0.9])