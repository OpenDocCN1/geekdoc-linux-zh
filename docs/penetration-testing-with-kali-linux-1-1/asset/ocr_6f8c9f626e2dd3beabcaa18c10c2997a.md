web server configurations, specifically **php.ini** values such as *register_globals* and *allow_url_wrappers*, make a considerable difference in how these vulnerabilities can be exploited.

> *The php.ini file on the Windows 10 lab machine can be found at C:\xampp\php\php.ini. Before making any changes to this file, consider making a backup.*

Note that directory traversal vulnerabilities are often used in conjunction with LFI’s, specifically to specify the file used in the LFI payload.

# 9.4.4.1 *Identifying File Inclusion Vulnerabilities*

File inclusions can be discovered in the same way as directory traversals. We must locate parameters we can manipulate and attempt to use them to load arbitrary files. However, a file inclusion takes this one step further, as we attempt execute the contents of the file within the application.

We should also check these parameters to see if they are vulnerable to remote inclusion (RFI) by changing their values to a URL instead of a local path. We are less likely to find RFI vulnerabilities since the default configuration for modern PHP versions disables remote URL includes, a key feature we need to execute remote code. However, we should still test for RFIs as they are often easier to exploit than LFI’s. We can use Netcat, Apache, or Python to handle the request just like we did with XSS. We may need to try hosting our payloads on different ports since any remote connection initiated by the target server may be subject to internal firewalls or routing rules. Some trial and error may be necessary.

# 9.4.4.2 *Exploiting Local File Inclusion (LFI)*

Let’s return to the sample application on our Windows 10 lab machine. We will pick up where we left off with the directory traversal attack and take a look at the source code of **menu.php** to clarify what we are dealing with:

```
37 < ?php
    38     $file  = $_GET["file"];
    39     include $file; ?>
```

*Listing 295 - Code excerpt from menu.php*

The application reads in the *file* parameter from the request query string and then uses that value with an *include*²⁷⁶ statement. This means that the application will execute any PHP code within the specified file. If the application opened the file with *fread* and used *echo* to display the contents, any code in the file would be displayed instead of executed.

We might be able to push this vulnerability to remote code execution if we can somehow write PHP code to a local file. Since we can't upload a file to the server, what options do we have?