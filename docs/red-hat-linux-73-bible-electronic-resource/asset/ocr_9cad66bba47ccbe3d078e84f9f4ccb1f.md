xterm command is used to log in to another computer. The title reminds you that you are not working on your own computer within that window, because you're logged in remotely.)

# ## Example four

X resources can also be set on a command line. The following is an example of an -xrm option being used to set resources for an xterm window.

```
$ xterm -xrm "XTerm*cursorColor:Blue"
```

This command opens an xterm window with the color of the cursor set to blue. You can set any xterm resource using the -xrm option. Try a few others, such as -xrm XTerm*background:Red or -xrm XTerm*foreground:Yellow. You can have more than one resource set at a time, but each must be preceded with -xrm.

> **CAUTION:** Be careful not to set background, foreground, and other adjacent items to the same color. If your text, cursor, or other items seem to have disappeared, they may just be set to the same color.

# # X resource files

When you specify a resource for an X client, that resource follows a fairly simple form. It consists of class name, attribute, and a value. The class name is just the name of the application with the first letter capitalized. Some class names that begin with the letter x, however, capitalize the second letter as well (for example, the class name for the xterm application is XTerm). The attribute identifies the element within that application. The value is what that element is set to.

Here is an example of an X resource:

```
XTerm*background: Red
```

The object of this attribute is the xterm command. The attribute is the background. The value sets the background to red. X resources that are specific to a particular client are organized in a hierarchy, in what is called a widget class. To find this hierarchy for an X client, check its man page and look for a WIDGETS heading. (Not all man pages have this heading.)

> **TIP:** To see the widget tree for an X client that is running, use the editres command. From editres, choose Commands \u2192 Get Tree, and then click the window of the client for which you want to see resources. To see an extensive list of resources, try clicking the editres window itself.

Because the hierarchy of resources can allow long names, you can use an asterisk in a resource name for what is called a *loose binding*. This means that any number of characters can be matched by the asterisk (as an asterisk is used as a wildcard in the shell). So, in the example, any resource that ends with the attribute *background* for the *XTerm* class will be *Red*.

If you want to be more specific in how you match a resource name, use a period (.) to create a *tight binding* in a resource name. A tight binding enables you to be more specific about the