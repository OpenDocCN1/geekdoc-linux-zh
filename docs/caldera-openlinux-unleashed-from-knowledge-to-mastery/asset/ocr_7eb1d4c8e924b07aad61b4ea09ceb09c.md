| Commands | Description |
| :--- | :--- |
| getoutput(string) | Very similar to getstatusoutput() but returns a string containing the output of the executed command, but no integer exit status. Here is an example: |

```python
>>> import commands
>>> commands.getstatusoutput('pwd')
(0, '/home/drobins')
```

# Where to Go from Here

This is the end of our Python tutorial, and I hope you’ve enjoyed the ride. We would like to provide you with instruction regarding further study so that you can continue to develop your Python programming skills.

# http://www.python.org

The Python Web site is loaded with excellent documentation. The Library Reference is recommended reading; it contains a complete listing of all standard Python modules and their associated functions. Simply browsing this list will whet your appetite for pushing Python to its limits! To get there, go to http://www.python.org; click on Documentation and then Library Reference. You will notice that the Documentation page contains a complete Language Reference as well as a Tutorial and FAQ. Use this documentation; it is very well written and covers many more topics than we can touch on in this short introductory text.

# Download the Docs

Even though http://www.python.org offers a full set of documentation online, if you plan to do any extensive Python development, you are encouraged to download the entire set of HTML documentation that is made available in a .tar.gz archive. By extracting the documentation to your local hard drive, you will be able to browse it faster and take some load off the Python Web site. You can browse the documentation in Netscape or Lynx by specifying a URL like this:
`file:///tmp/downloads/python-docs/index.html`

You can then browse the Python documentation directly from your hard drive, without setting up a Web server.

![](bbox=[0.83, 0.66, 0.98, 0.87])