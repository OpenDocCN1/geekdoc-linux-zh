# Working with the Shell

An example of the ln command to create a link can be seen here:

```
> ln -s /priv/home/rob/storage/HTML/123456789ABC.htm /etc/HTMLLAB/easy
```

If you were to do this, you would create a link named “easy” in the HTMLLAB directory that would be linked to the very long and not easy to remember HTML file in your stored HTML directory.

That's it! Creating a link, and now you not only know how to do it, but a practical reason why you should. Our last discussion in this lesson focuses on the proper way of using relative or absolute paths.

# Knowing the Right Path

We discussed the difference between relative and absolute paths in Lesson 5. By managing data using commands as cp and mv, you can also specify different paths when issuing the command. There are shortcuts and other tips (that could fill 50 of these books) that can help you be more productive.

It is very important to remember that when you give a filename as an argument to a Unix command, the filename can be either a relative or absolute path to the file. Consider this when you type out your command. Sometimes you may not be specifying the command properly and that is why it's failing: for example, if relative and absolute paths either use / or not, this may cause you to issue the command incorrectly and possibly give you an error message. If this happens, review the previous lesson on paths and apply that knowledge to your commands as you continue to learn and use them.

# Summary

In this lesson you learned more file management skills, which will serve as building blocks for the next few chapters in which you will learn to read and edit files.

At this point, you should be able to log into your Unix system and manage the locally stored data on it, and to move, copy, and delete data files.