the WAIS top directory and running the makefile (enter the command make).

Next, examine the Gopher Makefile.config file and look for the WAISTYPE variable. It should be defined on a line like this:

```
WAISTYPE = #-DFREEWAIS_0_4
```

Then, you have to link the Gopher and WAIS services. Suppose your Gopher source directory is /usr/gopher/source and the WAIS source directory is /usr/wais/source. You can link these services by entering the following commands:

```
cd /usr/gopher/source
ln -s /usr/wais/source/include ./ir
ln -s /usr/wais/source/client/ui .
ln -s /usr/wais/source/bin .
```

When Gopher is recompiled, it connects the links between Gopher and freeWAIS and allows the two services to interwork.

# # Setting Up Your Gopher Directories

Gopher directories and files are quite simple to set up and follow standard naming conventions for the most part. Before you begin, though, you should know which documents and files are to be provided through Gopher to other users, and you should be able to write a short description of each. (If you don't know the contents of a file, either read it or get the author to summarize the file for you.) For simplicity, let's assume you will use only a single directory for all your Gopher documents.

Begin by changing to the top directory you use for your Gopher directories (which you may have to create if you haven't already done so). This directory should not be where the Gopher source and configuration files are located, for convenience. Simply choose a useful name and create the directory. For example, to create the Gopher home directory /usr/gopher/data, issue a standard mkdir command:

```
mkdir /usr/gopher/data
```

Change into your Gopher directory and copy the files you want to make available into it. When you have done that, you can create a descriptive filename for each file (instead of the more obtuse filenames usually used) up to 80 characters long. For example, if you have a filename called q1.sales, you may want to rename it to Company_Sales_1887_01 to help users identify the contents a little more easily.