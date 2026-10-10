# # Chapter 8
# Printers and printing

In this chapter we will learn more about printers and printing files. After reading this part, you will be able to:

+   * Format documents
+   * Preview documents before sending them to the printer
+   * Choose a good printer that works with your Linux system
+   * Print files and check on printer status
+   * Troubleshoot printing problems
+   * Find necessary documentation to install a printer

# ## 8.1 Printing files

# ### 8.1.1 Command line printing

# #### 8.1.1.1 Getting the file to the printer

Printing from within an application is very easy, selecting the Print option from the menu.

From the command line, use the lp or lpr command.

```
```
lp file(s)
lpr file(s)
```
```

These commands can read from a pipe, so you can print the output of commands using

```
```
command | lp
```
```

There are many options available to tune the page layout, the number of copies, the printer that you want to print to if you have more than one available, paper size,