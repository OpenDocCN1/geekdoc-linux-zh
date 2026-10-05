# system-config-printer: CONFIGURING A PRINTER 553

![](bbox=[0.343, 0.07653499999999999, 0.793, 0.396535])

Figure 14-5 Selecting a printer manufacturer

use an LPD/LPR printer, use the form `lpd://hostname/printer-name`; for an HP JetDirect-compatible network printer, use the form `ipp://hostname/printers/printer-name`; use `socket://hostname`. Replace `hostname` with the name of the host it is attached to (the server), or for a network printer, the name of the printer. You can specify an IP address instead of `hostname`. Replace `printer-name` with the name of the printer on the server. Give the command `ipstat -p` on the server to display the names of all printers on that system. After selecting or specifying a printer, click the button labeled **Verify** (if present) to make sure the printer is accessible and click **Forward**. The system-config-printer utility searches for a driver for the

Next the utility may ask you which printer options you want to install. Specify the options and click **Forward**.

If system-config-printer displays the Choose Driver screen of the New Window (Figure 14-5), you can specify a printer manufacturer (such as HP). Typically system-config-printer selects the manufacturer automatically. Alternatively, you can specify a PPD file (page 561) or search for a driver to download. Click **Forward**.

The next screen (Choose Driver; Figure 14-6, next page), which system-config-printer may not display, allows you to specify the model of the printer and select which driver you want to use (if more than one is available). Again, these selections are usually highlighted automatically.