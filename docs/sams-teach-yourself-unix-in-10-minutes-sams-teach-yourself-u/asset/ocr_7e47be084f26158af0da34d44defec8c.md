+   - `.tex`—A TeX formatted file. TeX is a page layout language that is sometimes used to store program documentation. Look to the `tex` program, or the `latex` program, to work with these files.
+   - `.dvi`—The result of a TeX formatted file, somewhere between the markup language and the actual paper output. DVI actually is intended to be a device independent file which allows for similar display of marked up data on any platform. To view a dvi file, try the `xdvi` program if you're running the X Window System, `dvips` or `dvips` if you'd like to print the documentation, or `dvi2tty` if you're stuck on a text-only terminal.

That covers most of the cases that you'll encounter. If you run into a file format that doesn't appear to be included here, look around for an accompanying README.TXT, or README.1ST file—these are likely to contain information on how to make use of the unknown files.

# SUMMARY

Your UNIX computer is likely to be populated with a large number of documentation files, and more documentation comes with every new piece of software. This lesson should have given you a clear picture of the many different ways you can display files, or portions of files. Here's a review:

+   - `cat`—The concatenate command displays all the files you specify, one after the other. It does not pause at the end of pages.
+   - `more/less`—more and less are known as pagers. They page through their input files, one screen at a time. less offers the ability to scroll backwards through files, unlike more, which provides forward-only viewing.
+   - `head`—Displays the first few lines of a file. This is useful when you're trying to look at header information in files such as email messages.