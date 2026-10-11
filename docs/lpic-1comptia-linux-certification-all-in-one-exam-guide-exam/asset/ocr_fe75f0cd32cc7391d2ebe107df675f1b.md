# Figure 16-2
Sending a print job

![](bbox=[0.35, 0.08, 0.85, 0.43])

First, an application on the client system generates a print job and sends it to the cupsd daemon on the server. The daemon saves the job in the spooling directory. Print queue and filter information from the print job are saved in `/var/spool/cups`. The file is named with a `c`, concatenated with a print job number assigned by cupsd. The document to be printed is also saved in `/var/spool/cups`. This time, however, the file is named with a `d`, concatenated with the print job number assigned by cupsd.

Next, the print job is sent to the filter for conversion to the appropriate PDL. Once that's done, the converted print job is sent from the filter to the backend, which forwards the job to its connected printer. After sending the job to the printer, the backend notifies the cupsd daemon and the print job is deleted from the print queue.

Now that you know how CUPS printing works, I need to discuss how to install the service on your Linux system. Let's do that next.

# Installing CUPS

Unlike the services we reviewed earlier in this chapter, there's a pretty good chance that your Linux distribution installed the packages required to provide CUPS printing by default. As we said earlier, CUPS is the default printing system used by most modern Linux distributions.

If your distribution didn't install CUPS for some reason, use the package installation utility of your choice to install the following packages (along with any dependent packages):

+   - cups
+   - cups-client (optional)
+   - cups-drivers