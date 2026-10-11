directory to the HPLJ2 printer I just created, I would enter lp -d HPLJ5 ./myfiles at the shell prompt, as shown here:

```
ws1:~: $ lp -d HPLJ2 ./myfiles
request id is HPLJ2-2 (1 file(s))
ws1:~: $
```

As you can see in this example, the job is created and assigned an ID, in this case HPLJ2-2. The job is added to the print queue and sent to the printer. The lp utility includes a variety of options besides -d that you can use to create print jobs, including the following:

+   - -n x  Prints x number of copies
+   - -m  E-mails a confirmation message to my local user account when the job is finished printing
+   - -q  Sets the priority of the print job
+   - -o landscape  Prints the file landscape instead of portrait
+   - -o sides=2  Prints the file double-sided on a printer that supports duplexing

You can also configure other Linux systems to print to the CUPS printer. Simply configure a new printer, but specify that it listen for CUPS announcements. The CUPS printer you configured should be displayed within 30 seconds. After selecting it, all print jobs sent to that printer will be redirected over the network connection to your CUPS printer.

In addition, if you've installed Samba on your system, then your CUPS printers are automatically shared. You can connect to them from Windows workstations and submit print jobs. Now that's cool!

Let’s next discuss how to use command-line tools to manage your CUPS printers.

# ### Using Command-Line Tools to Manage CUPS

In addition to the CUPS web-based administration utility, you can also use a variety of command-line tools to configure CUPS. To view CUPS printer information, you can use the lpstat utility. One of the most useful options you can use with lpstat is -t.

This will cause lpstat to display all information about all CUPS printers on the system, as this next example shows:

```
ws1:~: $ lpstat is -t
scheduler running
no system default destination
device for HPLJ2: paralle1:/dev/lp3
HPLJ2 accepting requests since Fri 13 May 2011 10:57:13 AM MDT
printer HPLJ2 is idle, enabled since Fri 13 May 2011 10:57:13 AM MDT
      Printer is now online.
ws1:~: $
```

This shows the default CUPS printer (HPLJ2), how it’s connected (/dev/lp0), the print job currently being processed (if any), and a list of pending print jobs.