![](bbox=[0.21, 0.08, 0.77, 0.34])

As you can see, the application offers you a list of printers to choose from – the list shown above includes an entry for the **pmtf_queue-1** printer that we configured earlier. It also includes a **Generic Printer** entry – if you choose this, then the application will send the print job to your "default" printer (the one that your machine is configured to use automatically).

You'll need to configure the "default" printer before you use if for the first time; you can do this through the Openoffice Printer Setup tool. Select **Main Menu | Office | Openoffice.org Printer Setup**, select the **Generic Printer** entry in that dialog, and click the **Properties** button:

![](bbox=[0.08, 0.53, 0.92, 0.78])

In the resulting **Properties of Generic Printer** dialog, the default command in the **Select Command** section is `lpr` – this will send printer jobs via the `lpr` command to `/dev/lp0` as the default print queue. Change the command to `lpr -P printername`, where `printername` is the name you gave to your printer. Then click **OK** to save these settings.

Now you can return to your OpenWriter application, select **File | Print**, and select the **Generic Printer** option in the Print dialog to send the job to that printer.