Since we know the application is running on a Windows system, let's update our payload to target the Windows **hosts** file. This is a useful file to target on Windows systems since it is reliable and accessible by any user.

Let's change the parameter value to `c:\windows\system32\drivers\etc\hosts` and submit the URL:

```
http://10.11.0.22/menu.php?file=c:\windows\system32\drivers\etc\hosts
```

*Listing 294 - Updating the URL for Windows hosts file*

After submitting this URL in our browser, the page includes the content of the **hosts** file:

![](bbox=[0.13, 0.28, 0.87, 0.48])

Excellent. It appears this directory traversal vulnerability allows us to read files of any type, including those outside the web root directory.

# ## 9.4.3.2  Exercise

+   1.  Exploit the directory traversal vulnerability to read arbitrary files on your Windows 10 lab machine.

# ## 9.4.4  File Inclusion Vulnerabilities

Unlike directory traversals that simply display the contents of a file, file inclusion<sup>275</sup> vulnerabilities allow an attacker to include a file into the application’s running code.

In order to actually exploit a file inclusion vulnerability, we must be able to not only execute code, but also to write our shell payload somewhere.

Local file inclusions (LFI) occur when the included file is loaded from the same web server. Remote file inclusions (RFI) occur when a file is loaded from an external source. These vulnerabilities are commonly found in PHP applications but they can occur in other programming languages as well.

The exploitation of these vulnerabilities depends on the programming language the application is written in and the server configuration. In the case of PHP, the version of the language runtime and

<sup>275</sup> (Wikipedia, 2019), https://en.wikipedia.org/wiki/File_inclusion_vulnerability