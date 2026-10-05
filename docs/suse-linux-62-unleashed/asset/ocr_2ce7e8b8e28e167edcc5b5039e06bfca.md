# Graphics, Multimedia, and Productivity Tools
PART IV

Computers are supposed to help us be more productive and make things easier. One way the computer can help is by doing our office and administrative work. The computer doesn't forget to remind us that we have an appointment. The computer makes it really easy to reprint a document that your bonehead cube-mate just spilled coffee on.

This chapter covers Linux-based software that can help you increase your productivity, making your work look snazzy, create databases, and help you do all this as quickly as possible.

# A Note about Software Packaging

As discussed earlier, many programs come in a package format. This packaging allows you to install a binary version of the software and not worry with many of the details of compiling and linking a program. Typically, you may find these programs in the RPM format. RPM is the Red Hat Package Manager, a format made popular by Red Hat Software and originally included with its distribution of Linux. Several other distributions have been to use this system, including SuSE, the topic of this book.

![](bbox=[0.153, 0.477, 0.903, 0.513])

> Check out http://www.rpm.org or Maximum RPM (ISBN 0-672-31105-4) for further details on the Red Hat Package Manager.

In other cases, such as with WordPerf8, the software may provide its own installation program and provide binary software only in a proprietary format.

# Advantages of Packages

Using packaged software can remove the difficulties of finding, downloading, and compiling software. Often, example configuration files and documentation are included in the package, making an a a breeze. The package manager program can unpack the software, place the necessary files in the proper location, and keep a record of its transactions. RPM actually keeps track of all of your software (that it installs) and helps prevent from deleting programs that may be needed by other programs (dependencies).

Also, for the hard-core hacker, the source code to many Open Source software programs is available in the RPM format. This option allows you to get all the pieces that you need, review the source code, and still have full control of compiling and linking the program. What a deal!