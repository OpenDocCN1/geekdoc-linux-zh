+   3. Select Network Printer Windows Printer via SAMBA in the left pane of that window by clicking that entry once and then click the Browse button in the top-right corner of the page.

+   4. In the SMB Browser window that appears (Figure 10-5), navigate your way to the printer you want. Sometimes it takes a while for the information to load, so hang tight if things seem to have stalled. When you find the printer you're looking for, select it and then click OK. Once you're in the New Printer window, click the Forward button.

+   5. Now continue from Step 4 in “Manually Configuring Printers” on page 182.

![](bbox=[0.633, 0.068, 0.856, 0.307])

Figure 10-5: Browsing for printers connected over a Windows network

# For the Driverless Among You

As I mentioned, Linux does not yet have built-in support for a few printers. If you find yourself with such a printer, you can take a few routes in order to get things working.

# Checking the Connections

You'd be surprised how many times I have triumphantly solved someone's printer problems by simply turning on the printer or wiggling or unplugging the USB or parallel connectors. Printers that are powered down and/ have loose connections are often to blame the printer's model name fails to appear in the first page of the printer setup.

If that approach fails, browse to http://www.openprinting.org/printers/ because sometimes Linux can support certain printers only if they are connected via the parallel port, or if they work via USB in other systems.

# Trying Your Windows Drivers

If your printer came with an installation device, you might want to see whether you can find a driver for it there. The driver on such device should end in .ppd (for “PostScript printer description”). To use one of these drivers, trying your printer as described earlier, but when you get to the New printer where you select your printer's make, click the Provide PDF file option. Then try to locate the appropriate file by clicking the button that says (None) in the middle of the page. If you find your driver, click the Forward button and then continue the printer setup.