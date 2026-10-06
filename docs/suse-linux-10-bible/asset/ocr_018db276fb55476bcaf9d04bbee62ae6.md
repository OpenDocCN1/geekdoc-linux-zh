# Chapter 19 ✦ Setting Up Printing with CUPS 539

If you click the link Do Administrative Tasks or other links that require administrative privileges, an authentication dialog box is displayed (see Figure 19-9).

![](bbox=[0.181, 0.19, 0.48, 0.385])

Figure 19-9: The CUPS web interface with authentication dialog box

The SUSE default settings will not allow you to get past this point unless you have created a CUPS user from the command line using a command like the following:

```
lpasswd -a printman
```

This adds (-a) a CUPS user and prompts you for a password (it's rather fussy about what kind of password it will accept). After doing this, printman is a CUPS user. printman does not need to be a user in /etc/passwd. This is rather like setting up HTTP authentication. Now you can log into the administrative interface as this user and administer the CUPS server. When you logged in, you can perform all administration tasks from the web interface, including adding printers. The changes you make will then be written back to the CUPS configuration files.

The user information is specific to CUPS and is stored in the file /etc/cups/passwd.md5.

# Working with Classes in CUPS

One of the nice features of CUPS is the fact that you can create a class of printers (for example, a group of printers in a certain physical location). The class will consist of a set of printers to which the CUPS server can print, whether locally connected or across the network. After a class is set up, users' print jobs will be printed on any one of the printers in the class to which they have access.