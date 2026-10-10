# **Manual pages**

Linux makes available a set of pages that tells you all about every single command– what they do, how they work, how to run them and the command line arguments that each one will accept. Some of them will be a little difficult to understand for a newcomer to Linux, but they are consistent. Once you get the hang of a few, they will start to mean something to you and you will find them easier to work with. Manual pages are invoked with this command:

man <command to look up>

For example:

man ls

Name

ls - list directory contents

Synopsis

ls [option] ... [file] ...

# *Searching*

You can search through the manual pages for a specific keyword. This is helpful if you need a reminder of what command you need – when you know what you want to do but aren’t certain of the command that you need to use. You might need to try this a few times before you find what you’re after. You also may find that the particular keyword you are searching for shows up in a number of pages, and then you’ll have to sift through them to find the right one. The syntax is:

man -k <search term>

You can also search inside of a manual page. While you are on a page and you want to search for something on that page, press the forward slash (/) button and follow it up with the search term. Press enter and your results will appear. If there are numerous instances of the search term, you can press ‘n’ to move through them.