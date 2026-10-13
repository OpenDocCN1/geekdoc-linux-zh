You may not always have access to the GUI, especially when working from a remote system. In any case, text-based browsers work more quickly. The standard text-based browser for Red Hat is elinks. Once the package is installed, you can use it from the command line to open the web site of your choice. For example. Figure 2-19 illustrates the result of the elinks http://www.mheducation.com command.

To exit from elinks, press the ESC key to access the menu bar, and then press F | x and accept the prompt to exit from the browser.

If you configure a web server, the easiest way to make sure it works is with a simple text home page. No HTML coding is required. For example, I could add the following text to home.html

```
This is my home page
```

I could then run the elinks home.html command to view this text in the elinks browser. If you've set up an Apache file server on the /var/www/html/inst directory as discussed in Chapter 1, you can also use elinks to review the files copied to that server with the following command:

```
$ elinks http://192.168.122.1/inst
```

# FIGURE 2-19

The elinks browser

![](bbox=[0.22, 0.68, 0.92, 0.87])