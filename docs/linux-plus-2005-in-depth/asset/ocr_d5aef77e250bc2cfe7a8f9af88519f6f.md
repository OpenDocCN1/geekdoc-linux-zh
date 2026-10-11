After the type of printer is chosen, you must supply the specific information about the printer. For a local printer, you must choose the port that connects to the printer, such as `/dev/lp0` shown earlier Figure 11–4. For remote printers, you need to specify the name or IP address of the remote server, printer name, or printer port.

Following this, you are prompted to choose the model of your printer, as shown in Figure 11–6, and confirm the printer creation, as shown in Figure 11–7. After the printer has been created, the Printer Configuration tool prompts you to print a test page and displays a line that represents the printer, as shown in Figure 11–8.

You can modify all printer settings by clicking the Edit button from Figure 11–8, or print a test page by selecting the appropriate test page from the Test menu. After adding or modifying printer settings, you must choose Apply to restart the cups daemon for the settings to take effect. Also notice from Figure 11–8 that printer1 is the default printer and is not shared to network users. To configure printer sharing, simply choose Sharing from the Action menu in Figure 11–8, select "This queue is available to other computers," and specify which computers are allowed to print to the printer, as shown in Figure 11–9.

![](bbox=[0.15, 0.45, 0.66, 0.65])

**FIGURE 11-6** *Selecting the printer model for a new printer*

![](bbox=[0.15, 0.69, 0.66, 0.91])

**FIGURE 11-7** *Completing the creation of a new printer*