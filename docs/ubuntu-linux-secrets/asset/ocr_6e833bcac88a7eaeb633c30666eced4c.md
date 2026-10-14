![](bbox=[0.2, 0.15, 0.8, 0.55])

Figure 21-8: The phpinfo() function output.

# Tomcat

If you chose to install Tomcat from the Ubuntu server installation menu, it installed Tomcat 6, the latest release of the Tomcat server. The Tomcat 6 server is called a servlet container. A servlet container has the ability to load Java servlets and process JavaServer Pages from a web interface.

The following sections describe the Tomcat environment on the Ubuntu server and show how to use Tomcat to serve JavaServer Pages and servlets.

> Secret
> 
> Just as with the Apache web server installation, you can also install the Tomcat server in the Ubuntu workstation distribution; however, Tomcat isn't recommended for a production web server.
> 
> If you do decide to install the Tomcat server in an Ubuntu workstation installation, don't install it using the Synaptic Package Manager. The Tomcat packages available in the workstation software repositories aren't the same as the ones in the server repositories.
> 
> Instead, use the tasksel utility from a Terminal command prompt:
> 
> sudo tasksel
> 
> Select the Tomcat entry from the menu, being careful not to deselect any already-selected entries.

```
sudo tasksel
```